# Frigate - Open-Source NVR with AI Detection

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Active  
**Tags**: nvr-system, surveillance, camera-monitoring, ai-detection, edge-device, proxmox-deployment

## Overview

Frigate is an open-source Network Video Recorder (NVR) for camera surveillance with AI-powered object detection. Designed for self-hosted deployment with hardware acceleration support and integrates with [[Proxmox VE Homelab Management]].

## Problem/Motivation

Wants to deploy Frigate again with current hardware setup. Has Reolink 8xx PoE cameras + Wyze cameras that would work well with Frigate. Detailed Proxmox LXC setup available matching current infrastructure.

## Current Hardware

- **Cameras**: Reolink 8xx PoE + Wyze cameras
- **Hypervisor**: Proxmox VE
- **GPU**: Intel iGPU (11th gen or similar)
- **Acceleration**: USB Coral EdgeTPU
- **Storage**: Network shares available

## Key Features

- **Real-Time Detection**: Object detection on video streams
- **AI-Powered**: Uses EdgeTPU for efficient inference
- **Hardware Acceleration**: Intel iGPU, GPU, TPU support
- **Event Recording**: Triggered recording on detected objects
- **24/7 Recording**: Optional continuous recording
- **Snapshots**: Auto-generate snapshots on events
- **Multi-Camera**: Support for many simultaneous streams
- **RTSP Support**: Compatible with most IP cameras
- **API**: REST API for integrations
- **Notifications**: Alert on detections

## Deployment Architecture (Proxmox LXC)

### Setup Overview

```
Proxmox Host
├── Intel iGPU
├── USB Coral (EdgeTPU)
└── LXC Container (Unprivileged)
    ├── Docker
    │   └── Frigate Container
    │       ├── Detection
    │       ├── Recording
    │       └── Web UI
    ├── GPU Access (renderD128)
    ├── USB Device Access (Coral)
    └── Network Storage (CIFS mount)
```

## Proxmox LXC Setup (Unprivileged)

### Prerequisites

- Proxmox host with Intel GPU
- USB Coral connected
- Network share available
- Ubuntu 22.04 LXC template

### Setup Steps

#### 1. Create Unprivileged LXC Container

```bash
# In Proxmox UI:
# - Download Ubuntu 22.04 template
# - Create CT with Unprivileged checked
# - Set strong password
# - Allocate CPU/RAM/Disk
# - Configure networking (DHCP)
```

#### 2. Pass Through USB Coral

Edit LXC config file (`/etc/pve/lxc/XXX.conf`):

```bash
# Identify Coral bus number
lsusb  # Note the bus

# Add to config
usb0: host=1a6e:089a,usb3=1
usb1: host=18d1:9302,usb3=1
lxc.cgroup2.devices.allow: c 189:* rwm
lxc.mount.entry: /dev/bus/usb/004 dev/bus/usb/004 none bind,optional,create=dir
```

**Note**: Replace bus number (004) with your Coral's bus number from `lsusb`

#### 3. Pass Through Intel iGPU

On Proxmox host:

```bash
# Verify GPU
lspci -nnv | grep VGA

# Check DRI devices
ls -l /dev/dri
# Note: card0 (major 226, minor 0)
#       renderD128 (major 226, minor 128)

# Set permissions
chmod 666 /dev/dri/renderD128
```

Edit LXC config (`/etc/pve/lxc/XXX.conf`):

```bash
lxc.cgroup2.devices.allow: c 226:0 rwm
lxc.cgroup2.devices.allow: c 226:128 rwm
lxc.mount.entry: /dev/dri/renderD128 dev/dri/renderD128 none bind,optional,create=file 0, 0
lxc.mount.entry: /dev/dri dev/dri none bind,optional,create=dir
```

**Persist after reboot** - Create udev rule:

```bash
# On Proxmox host
nano /etc/udev/rules.d/99-intel-chmod666.rules
```

Add:
```
KERNEL=="renderD128", MODE="0666"
```

#### 4. Pass Through Network Share

On Proxmox host:

```bash
# Create mount point
mkdir -p /mnt/lxc_shares/frigate_storage

# Add to /etc/fstab
//NAS_IP/SHARE_NAME /mnt/lxc_shares/frigate_storage cifs \
  _netdev,noserverino,x-systemd.automount,noatime,\
  uid=100000,gid=110000,dir_mode=0770,file_mode=0770,\
  username=USERNAME,password=PASSWORD 0 0

# Mount
mount /mnt/lxc_shares/frigate_storage
```

In LXC container console:

```bash
# Create group matching GID
groupadd -g 10000 lxc_shares
usermod -aG lxc_shares root
```

Edit LXC config:

```bash
mp0: /mnt/lxc_shares/frigate_storage/,mp=/opt/frigate/media
```

#### 5. Install Docker & Frigate

In LXC container:

```bash
# Update system
apt-get update && apt-get upgrade -y

# Install Docker
apt install curl
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh

# Test Docker
docker run hello-world
```

**Install Portainer** (optional, for web UI):

```bash
docker run -d \
  --name portainer \
  --restart on-failure \
  -p 9000:9000 \
  -p 8000:8000 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce:latest
```

Access at `http://CONTAINER_IP:9000`

#### 6. Frigate Configuration

Create folder structure:

```bash
cd /opt
mkdir frigate
cd frigate
mkdir media
mkdir storage
```

Create `config.yml` in `/opt/frigate/`:

```yaml
database:
  path: /db/frigate.db

mqtt:  # Optional - update if you have MQTT
  host: MQTT_IP
  user: mqtt_user
  password: mqtt_pass

detectors:
  coral:
    type: edgetpu
    device: usb

ffmpeg:
  output_args:
    record: -f segment -segment_time 10 -segment_format mp4 -reset_timestamps 1 -strftime 1 -c copy
  hwaccel_args:  # Intel iGPU acceleration
    - -c:v
    - h264_qsv

objects:
  track:
    - person

record:
  events:
    pre_capture: 7
    post_capture: 10

cameras:
  reolink_front:  # Reolink PoE camera
    ffmpeg:
      inputs:
        - path: rtsp://USER:PASS@REOLINK_IP:554/h264Preview_01_main
          roles:
            - detect
            - rtmp
        - path: rtsp://USER:PASS@REOLINK_IP:554/h264Preview_01_main
          roles:
            - record
    detect:
      width: 1280
      height: 720
    record:
      enabled: true
      events:
        retain:
          mode: active_objects
          default: 10
    snapshots:
      enabled: true
      retain:
        default: 10

  wyze_camera:  # Wyze camera
    ffmpeg:
      inputs:
        - path: rtsp://USER:PASS@WYZE_IP/live
          roles:
            - detect
            - rtmp
        - path: rtsp://USER:PASS@WYZE_IP/live
          roles:
            - record
    detect:
      width: 1280
      height: 720
    record:
      enabled: true
```

#### 7. Deploy Frigate Container

In Portainer, create new Stack with:

```yaml
version: "3.9"
services:
  frigate:
    container_name: frigate
    privileged: true
    restart: unless-stopped
    image: ghcr.io/blakeblackshear/frigate:stable
    shm_size: "64mb"
    devices:
      - /dev/bus/usb:/dev/bus/usb      # USB Coral
      - /dev/dri/renderD128             # Intel iGPU
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - /opt/frigate/config.yml:/config/config.yml
      - /opt/frigate/media:/media/frigate
      - type: tmpfs
        target: /tmp/cache
        tmpfs:
          size: 1000000000              # 1GB RAM cache
    ports:
      - "5000:5000"                     # Web UI
      - "8554:8554"                     # RTSP feeds
      - "8555:8555/tcp"                 # WebRTC
      - "8555:8555/udp"
    environment:
      FRIGATE_RTSP_PASSWORD: "secure_password"
```

Access UI at `http://CONTAINER_IP:5000`

## Camera Setup

### Reolink 8xx PoE

- **Stream URL**: `rtsp://USER:PASS@IP:554/h264Preview_01_main`
- **Resolution**: 2688×1520 (detect on lower res stream)
- **Codec**: H.264
- **Power**: PoE (simplifies cabling)

### Wyze Cameras

- **Stream URL**: `rtsp://USER:PASS@IP/live`
- **Resolution**: 1920×1080
- **Codec**: H.264
- **Note**: Requires RTSP firmware

## Hardware Acceleration

### Intel iGPU Options

**11th Gen Intel** (like in setup):
```yaml
hwaccel_args:
  - -c:v
  - h264_qsv
```

**10th Gen Intel**:
```yaml
hwaccel_args:
  - -hwaccel
  - vaapi
  - -hwaccel_device
  - /dev/dri/renderD128
  - -hwaccel_output_format
  - yuv420p
```

## Performance Tuning

### Memory Calculation

```
Shm-size = 250M × (# of cameras) + 75M
Example: 2 cameras = 250M × 2 + 75M = 575M
Use 64MB tmpfs cache for additional SSD wear reduction
```

### Detection Resolution

- **Detection**: Lower res stream (1280×720) for efficiency
- **Recording**: Higher res stream for quality
- **Two-stream approach** saves bandwidth and CPU

## Relevant Resources

- [blakeblackshear/frigate](https://github.com/blakeblackshear/frigate) ��� Official repository
- [Frigate Documentation](https://docs.frigate.video) — Complete docs
- [Frigate Proxmox Discussion](https://github.com/blakeblackshear/frigate/discussions/5773) — Setup guide
- [Coral EdgeTPU](https://coral.ai) — Hardware documentation
- Related topics: [[Proxmox VE Homelab Management]], [[GPU Hardware]], [[Network Cameras]], [[Surveillance]]

## Monitoring & Alerts

### Integration Options

1. **Home Assistant**:
   - Subscribe to MQTT events
   - Trigger automations
   - Send notifications

2. **Jellyfin**:
   - Archive clip previews
   - Organize by camera

3. **n8n Automation**:
   - Watch for specific detections
   - Trigger workflows
   - Send alerts

4. **Discord Webhooks**:
   - Instant notifications
   - Snapshot preview
   - Detection summary

## Next Steps

- [ ] Gather camera stream URLs
- [ ] Test Reolink camera connectivity
- [ ] Configure Wyze RTSP firmware
- [ ] Deploy Frigate container
- [ ] Fine-tune detection resolution
- [ ] Set up recording retention
- [ ] Configure event notifications
- [ ] Monitor performance and adjust

## Troubleshooting

### Common Issues

**GPU Not Recognized**:
- Verify `ls -l /dev/dri` shows renderD128
- Check chmod 666 permissions
- Verify LXC config device mounts

**USB Coral Not Found**:
- Verify `lsusb` shows device
- Check LXC USB device mounts
- Confirm bus number in config

**High CPU Usage**:
- Lower detection resolution
- Use hardware acceleration
- Reduce number of camera streams
- Increase detection frame skip

**Recording Issues**:
- Check disk space
- Verify network mount
- Check file permissions
- Review ffmpeg output

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*