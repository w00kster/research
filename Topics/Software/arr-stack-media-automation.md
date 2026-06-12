# *arr Stack - Automated Media Management

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Active  
**Tags**: media-management, automation, homelab, *arr-ecosystem, sonarr, radarr, lidarr

## Overview

The *arr stack encompasses a family of PVR (Personal Video Recorder) and media management applications for automating downloads and organization of movies, TV shows, music, comics, and other media. Currently running on Proxmox PVE with Jellyfin backend.

## Included Applications

### Video Management

- **Sonarr**: TV series automation
- **Radarr**: Movie automation
- **Lidarr**: Music automation

### Comic & Book Management

- **Mylar3**: Comic book automation
- **Kapowarr**: Comic book with Komga integration
- **Kavita**: E-book and comic reader
- **Stump**: Comic/manga reader

### Game Management

- **Questarr**: Game automation and management

### Media Customization

- **One Pace for Jellyfin**: One Piece episode editor

## Current Deployment

### Existing Setup

- **Hypervisor**: Proxmox VE
- **Primary Media Server**: Jellyfin
- **Integration**: Tailscale for remote access
- **Monitoring**: Pulse for infrastructure visibility

### Infrastructure Components

```
Proxmox VE
├── Jellyfin (media server)
├── Sonarr (TV automation)
├── Radarr (movie automation)
├── Lidarr (music automation)
├── Prowlarr (indexer hub)
├── *arr comic tools (Mylar3, Kapowarr, Kavita, Stump)
├── Questarr (game management)
└── Download clients (qBittorrent, Usenet)
```

## Comics & Books

### Management Tools

| Tool | Focus | Features |
|------|-------|----------|
| **Mylar3** | Comic automation | Indexing, searching, auto-download |
| **Kapowarr** | Comic with Komga | Web UI, metadata, library integration |
| **Kavita** | E-book reader | Dark mode, offline, OPDS support |
| **Stump** | Comic/manga reader | Modern UI, progress tracking |

### Evaluation Criteria

- [ ] Library organization approach
- [ ] Metadata accuracy (issue numbers, covers)
- [ ] Community size and activity
- [ ] Integration with Jellyfin
- [ ] Performance with large libraries
- [ ] Mobile app availability

## Game Management

### Questarr

- Game library automation
- Integration with multiple platforms
- Metadata and artwork management
- Community sourcing of games

## Content Customization

### One Pace for Jellyfin

**Purpose**: Edited One Piece episodes removing filler content

- [ ] Install plugin for Jellyfin
- [ ] Configure episode mapping
- [ ] Test playback integration
- [ ] Verify subtitle/audio handling

## Relevant Resources

- [Mylar3](https://github.com/mylar3/mylar3) — Comic automation
- [Kapowarr](https://github.com/Casvt/Kapowarr) — Comic with Komga
- [Kavita](https://github.com/Kareadita/Kavita) — E-book reader
- [Stump](https://github.com/stumpapp/stump) — Comic/manga reader
- [Questarr](https://github.com/Doezer/Questarr) — Game automation
- [One Pace for Jellyfin](https://github.com/McCio/one-pace-for-jellyfin) — One Piece editor
- [r/arrsociety](https://www.reddit.com/r/arrsociety/) — Community
- Related topics: [[Proxmox VE Homelab Management]], [[Jellyfin Media Server]], [[*arr Ecosystem]]

## Deployment Strategy

### Phase 1: Evaluation

- [ ] Review current *arr deployment
- [ ] Assess comic/book tool landscape
- [ ] Test Questarr in staging
- [ ] Evaluate One Pace integration

### Phase 2: Expansion

- [ ] Deploy selected comic tools
- [ ] Migrate existing comic library
- [ ] Configure automation rules
- [ ] Test Questarr integration
- [ ] Install One Pace plugin

### Phase 3: Optimization

- [ ] Monitor resource usage
- [ ] Fine-tune automation rules
- [ ] Maintain metadata accuracy
- [ ] Regular library cleanup

## Comic Tool Comparison

### Mylar3
**Best for**: Automated comic discovery and management
- Indexer integration
- Searching and searching
- Automatic downloads
- Metadata from multiple sources

### Kapowarr
**Best for**: Integration with Komga reader
- Modern web UI
- Komga compatibility
- Metadata enrichment
- Community-driven

### Kavita
**Best for**: Reading e-books and comics
- Full-featured reader
- OPDS support for mobile
- Dark mode and accessibility
- Progress tracking

### Stump
**Best for**: Comic and manga reading
- Modern interface
- Fast performance
- Progress indicators
- Collection management

## Configuration Considerations

### Storage Layout

```
/media/
├── Movies/
├── TV/
├── Music/
├── Comics/
│   ├── Marvel/
│   ├── DC/
│   └── Manga/
├── Books/
└── Games/
```

### Networking

- Internal access via Proxmox bridge
- Tailscale for remote access
- DNS records for local discovery
- Reverse proxy for unified access

## Learning Path

1. **Tool Evaluation**:
   - [ ] Test comics tools in Docker
   - [ ] Assess UX and features
   - [ ] Check documentation quality
   - [ ] Review community support

2. **Library Assessment**:
   - [ ] Current comic/book collection
   - [ ] Game library status
   - [ ] One Piece episodes to curate
   - [ ] Organization strategy

3. **Deployment**:
   - [ ] Create LXCs for new tools
   - [ ] Configure storage mounts
   - [ ] Set up automation rules
   - [ ] Test end-to-end workflows

4. **Maintenance**:
   - [ ] Monitor indexers
   - [ ] Handle metadata errors
   - [ ] Update tools regularly
   - [ ] Troubleshoot issues

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*