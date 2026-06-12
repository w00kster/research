# Tracearr - Multi-Server Media Monitoring

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Reference  
**Tags**: media-monitoring, plex, jellyfin, emby, homelab, stream-analytics, account-sharing

## Overview

Tracearr is a monitoring platform for Plex, Jellyfin, and Emby that consolidates multi-server dashboards into single interface. Tracks streams in real-time, provides playback analytics, detects account sharing, and offers comprehensive library analytics.

## Key Features

### Multi-Server Dashboard

- Connect Plex, Jellyfin, and Emby to single interface
- Unified view across all servers
- No more switching between apps

### Session Tracking

- Complete session history: who watched what, when, where, device
- Every stream includes geolocation data
- Real-time stream monitoring

### Stream Analytics

- Transcode vs direct play tracking
- Bandwidth usage monitoring
- Codec breakdowns and resolution stats
- Device compatibility scores
- Enhanced stream information

### Library Analytics

- **Overview**: Item counts, storage usage, growth charts
- **Quality**: Resolution and codec distribution tracking
- **Storage**: Usage predictions, duplicate detection, stale content, ROI analysis
- **Watch**: Engagement metrics, completion rates, viewing patterns, binge detection

### Live TV & Music

- Track live TV sessions and music playback
- Works across all server types

### Stream Map

- World map visualization of stream origins
- Filter by user, server, or time period

### Sharing Detection

Six rule types flag suspicious activity:

- **Impossible Travel**: NYC then London 30 minutes later
- **Simultaneous Locations**: Same account from multiple cities
- **Device Velocity**: Too many IPs in short window
- **Concurrent Streams**: Per-user limits
- **Geo Restrictions**: Block specific countries
- **Account Inactivity**: Notification for dormant accounts

### Trust Scores

- Users earn/lose trust based on behavior
- Violations drop scores automatically

### Real-Time Alerts

- Discord webhooks
- Custom notifications
- Instant rule triggers

### Additional Capabilities

- Public REST API (read-only)
- Swagger UI at `/api-docs`
- Bulk actions (multi-select operations)
- Data import (Tautulli, Jellystat migration)

## Problem/Motivation

Addition to existing homelab media stack. Currently runs Jellyfin with *arr stack on Proxmox. Tracearr provides advanced monitoring and sharing detection capabilities. Falls into "cool factor" category - useful for analytics but not critical for current setup. Complements [[Proxmox VE Homelab Management]] for infrastructure-level monitoring.

## Comparison with Alternatives

| Feature | Tautulli | Jellystat | Tracearr |
|---------|----------|-----------|----------|
| Watch history | ✅ | ✅ | ✅ |
| Statistics | ✅ | ✅ | ✅ |
| Session monitoring | ✅ | ✅ | ✅ |
| Transcode analytics | ✅ | ✅ | ✅ |
| Account sharing detection | ❌ | ❌ | ✅ |
| Impossible travel alerts | ❌ | ❌ | ✅ |
| Trust scoring | ❌ | ❌ | ✅ |
| Multi-server dashboard | ❌ | ❌ | ✅ |
| Plex support | ✅ | ❌ | ✅ |
| Jellyfin support | ❌ | ✅ | ✅ |
| Emby support | ❌ | ✅ | ✅ |

## Relevant Resources

- [connorgallopo/Tracearr](https://github.com/connorgallopo/Tracearr) — Official repository
- [Documentation](https://docs.tracearr.com) — Full docs
- [Docker Hub](https://ghcr.io/connorgallopo/tracearr) — Container images
- [Discord Community](https://discord.gg/a7n3sFd2Yw) — Support and community
- Related topics: [[Proxmox VE Homelab Management]], [[Media Server Stack]], [[Jellyfin]]

## Technical Stack

| Layer | Technology |
|-------|------------|
| Frontend | React 19, TypeScript, Tailwind, shadcn/ui |
| Charts | Highcharts |
| Maps | Leaflet |
| Backend | Node.js, Fastify |
| Database | TimescaleDB (PostgreSQL extension) |
| Cache | Redis |
| Real-time | Socket.io |
| Monorepo | pnpm + Turborepo |

**Design Notes**:
- **TimescaleDB**: Built for time-series data - handles long session histories efficiently
- **Fastify**: Measurably faster than Express, schema validation catches bad requests
- **Plex SSE**: Real-time Server-Sent Events for instant detection
- **Jellyfin/Emby**: Polling-based (no SSE support)

## Deployment

### Quick Start

```bash
curl -O https://raw.githubusercontent.com/connorgallopo/Tracearr/main/docker/examples/docker-compose.pg18.yml
echo "JWT_SECRET=$(openssl rand -hex 32)" > .env
echo "COOKIE_SECRET=$(openssl rand -hex 32)" >> .env
docker compose -f docker-compose.pg18.yml up -d
```

Access at `http://localhost:3000`

### Docker Tags

- `latest`: Stable (requires external DB/Redis)
- `supervised`: All-in-one stable
- `next`: Prerelease
- `nightly`: Bleeding edge

### Development

```bash
pnpm install
docker compose -f docker/docker-compose.dev.yml up -d
cp .env.example .env
pnpm --filter @tracearr/server db:migrate
pnpm dev
```

## Integration with Homelab

- [ ] Deploy on Proxmox PVE infrastructure
- [ ] Connect to existing Jellyfin instance
- [ ] Configure Discord webhook alerts
- [ ] Set up monitoring dashboards
- [ ] Integrate with Pulse for unified metrics
- [ ] Archive watch history from Tautulli if applicable
- [ ] Configure trust rules for known accounts

## Status

Cool-factor addition to homelab media stack. Not critical but provides advanced analytics and sharing detection capabilities beyond basic Jellyfin admin interface.

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*