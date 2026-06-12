# SoulSync - Self-Hosted Music Streaming

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Active  
**Tags**: music-streaming, self-hosted, spotify-alternative, pve-deployment, audio-streaming

## Overview

SoulSync is a self-hosted music streaming platform providing alternative to commercial streaming services. Long-term goal is to move away from Spotify and achieve full music library self-hosting.

## Problem/Motivation

Wants to transition music consumption to self-hosted infrastructure. SoulSync represents viable path to Spotify replacement within Proxmox homelab. Would integrate with existing [[Supertonic TTS]] and [[Proxmox VE Homelab Management]] infrastructure.

## Key Objectives

### Phase 1: Evaluation & Deployment
- [ ] Review SoulSync capabilities and requirements
- [ ] Assess library import options
- [ ] Design deployment on Proxmox
- [ ] Test with subset of music library
- [ ] Validate audio quality

### Phase 2: Migration
- [ ] Export Spotify library metadata
- [ ] Import into SoulSync
- [ ] Set up sync with Tailscale
- [ ] Configure mobile client access
- [ ] Validate playback across devices

### Phase 3: Full Replacement
- [ ] Sunset Spotify subscription
- [ ] Maintain offline backup
- [ ] Monitor for missing features
- [ ] Iterate on UI/UX

## Relevant Resources

- [Nezreka/SoulSync](https://github.com/Nezreka/SoulSync) — Official repository
- Related topics: [[Proxmox VE Homelab Management]], [[Jellyfin Media Server]], [[Self-Hosted Services]], [[Music Management]]

## Deployment Architecture

### Proxmox Integration

1. **LXC Container**:
   - [ ] Create dedicated LXC in Proxmox
   - [ ] Allocate CPU/memory based on requirements
   - [ ] Configure storage for music library
   - [ ] Set up network bridge for Tailscale

2. **Storage Strategy**:
   - [ ] Where to store music files (NAS, local storage)
   - [ ] Backup strategy for library
   - [ ] Metadata caching approach
   - [ ] Library organization format

3. **Networking**:
   - [ ] Tailscale integration for remote access
   - [ ] Local network access via Proxmox bridge
   - [ ] DNS configuration for local discovery
   - [ ] Port forwarding (if external access needed)

### Infrastructure Dependencies

- **Database**: Requirements (PostgreSQL, SQLite?)
- **Cache Layer**: Redis for performance
- **Media Format Support**: Codec requirements
- **Audio Engine**: Streaming bitrate options

## Music Library Management

### Import Options

- [ ] Spotify library export
- [ ] Local music files (FLAC, MP3, OGG)
- [ ] Other streaming service migration
- [ ] Metadata sources (MusicBrainz, discogs)

### Playback Clients

- [ ] Web UI
- [ ] Mobile app (iOS/Android)
- [ ] Desktop application
- [ ] DLNA/streaming protocol support

## Integration with Homelab

### Potential Synergies

- **Supertonic TTS**: Text-to-speech narration for playlists?
- **Open-WebUI**: LLM playlist recommendations
- **n8n**: Automation for library management
- **Jellyfin**: Unified media management dashboard

## Learning Path

1. **Initial Exploration**:
   - [ ] Review GitHub documentation
   - [ ] Test locally in VM
   - [ ] Evaluate feature set vs Spotify
   - [ ] Check community activity/support

2. **Library Assessment**:
   - [ ] Export current Spotify library
   - [ ] Count songs, artists, playlists
   - [ ] Identify missing tracks that need sourcing
   - [ ] Plan import strategy

3. **Proxmox Deployment**:
   - [ ] Container configuration
   - [ ] Storage setup and testing
   - [ ] Tailscale integration
   - [ ] Performance tuning

4. **Migration Execution**:
   - [ ] Import primary library
   - [ ] Test playback quality
   - [ ] Set up client access
   - [ ] Gradual transition from Spotify

## Technical Notes

**Streaming Quality**: Verify maximum bitrate supported and compare with Spotify Premium requirements.

**Metadata Accuracy**: SoulSync must handle metadata reliably for playlist management and searching.

**Playlist Preservation**: Ensure current playlists can be migrated or rebuilt in new system.

**Offline Listening**: Check if mobile app supports offline sync like Spotify.

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*