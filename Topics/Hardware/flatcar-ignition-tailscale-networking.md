# Flatcar Ignition Generator with Tailscale

**Category**: Hardware  
**Added**: 2026-06-12  
**Status**: Active  
**Tags**: networking, flatcar, ignition, tailscale, homelab, vm-provisioning, cloud-init

## Overview

Flatcar Ignition Generator with Tailscale is a tool for generating Flatcar OS ignition configurations that provision Tailscale exit nodes or subnet routers. Enables rapid deployment of Tailscale networking on bare metal or cloud VMs without build steps, API keys, or local tooling.

## Key Points

- **Zero Friction**: No build step, no provider API keys, no local tooling required
- **Static Binary**: Single HTML/JavaScript app - works anywhere
- **Multiple Providers**: Support for Vultr, DigitalOcean, Hetzner cloud platforms
- **Exit Nodes**: Deploy as Tailscale exit node for privacy/geographic routing
- **Subnet Routers**: Provide subnet access to Tailnet devices
- **Config as Code**: Ignition JSON output for infrastructure-as-code workflows
- **Auth Management**: Tailscale auth key integration with clear lifecycle

## Supported Providers

| Provider | Setup | Friction | Notes |
|----------|-------|----------|-------|
| **Vultr** | Flatcar native | Lowest | Easiest choice for beginners |
| **DigitalOcean** | Custom image import | Medium | Import Flatcar image first |
| **Hetzner** | Snapshot setup | Medium | Use hcloud-upload-image |

## Problem/Motivation

Interesting tool for expanding homelab infrastructure beyond Proxmox. Could leverage Binary Lane VMs (already paid for monthly) to extend Tailscale network and create geographic distribution for networking. Could integrate with [[Proxmox VE Homelab Management]] for hybrid infrastructure and [[Pulse - Proxmox VE Monitoring & Management]] for unified monitoring.

## Use Cases

1. **Expand Tailnet**: Add exit nodes for geographic diversity
2. **Subnet Access**: Provide LAN access to Tailnet devices
3. **Binary Lane Integration**: Use existing monthly-paid VMs to create exit nodes
4. **Infrastructure-as-Code**: Generate Ignition configs for repeatable deployments
5. **Multi-Cloud Routing**: Connect to multiple cloud providers via single Tailnet

## Relevant Resources

- [ironicbadger/flatcar-ignition-generator-tailscale](https://github.com/ironicbadger/flatcar-ignition-generator-tailscale) — Official repository
- [Flatcar Container Linux](https://www.flatcar.org/) — OS documentation
- [Tailscale Documentation](https://tailscale.com/docs/) — Network setup
- Related topics: [[Proxmox VE Homelab Management]], [[Tailscale Networking]], [[Infrastructure-as-Code]]

## Deployment Planning

### Binary Lane Integration

- [ ] Assess current Binary Lane VM status and costs
- [ ] Design Tailscale exit node placement strategy
- [ ] Generate Ignition configs for exit nodes
- [ ] Deploy test exit node to validate setup
- [ ] Monitor traffic and performance
- [ ] Document infrastructure changes
- [ ] Automate deployment with infrastructure tooling

### Infrastructure Expansion

- [ ] Map existing Tailnet topology
- [ ] Identify geographic routing needs
- [ ] Plan subnet router placement
- [ ] Test failover and redundancy
- [ ] Integrate monitoring with Pulse
- [ ] Document access policies

## Technical Notes

**Ignition Format**: Generated JSON complies with Flatcar Ignition specification. Config contains auth key - treat as secret until deployment.

**Auth Key Lifecycle**: Tailscale auth key embedded in config. Key should have appropriate TTL and be rotated after deployment to prevent reuse.

**Multi-Provider**: Same workflow across providers - only provider field changes in Ignition JSON.

**No Build Required**: App is static - can be hosted anywhere or run locally.

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*