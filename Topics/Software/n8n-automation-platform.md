# n8n - Open-Source Automation Platform

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Active  
**Tags**: automation, workflow-orchestration, no-code, integration-platform, business-automation

## Overview

n8n is a powerful, open-source workflow automation platform for connecting apps and automating processes. Provides visual workflow builder with 400+ integrations and ability to create complex automation without writing code.

## Problem/Motivation

Interested in exploring automation possibilities for homelab and potentially other use cases. n8n provides no-code/low-code approach to orchestrating complex workflows. Currently unclear on specific use cases but platform offers significant potential for:

- **Homelab Automation**: Coordinate services and tasks
- **Data Pipeline**: Move data between systems
- **Content Management**: Automate media workflows
- **Infrastructure**: Coordinate provisioning and configuration
- **Business Logic**: Implement workflows without custom code

## Key Features

- **Visual Workflow Builder**: Drag-and-drop node-based interface
- **400+ Integrations**: Pre-built connectors for popular services
- **Custom Code**: JavaScript/Python nodes for custom logic
- **Error Handling**: Retry logic, error branches, conditional flows
- **Scheduling**: Cron jobs and event triggers
- **Webhooks**: Trigger workflows from external sources
- **Database**: Built-in data persistence
- **Self-Hosted**: Full control over data and execution

## Use Case Exploration

### Potential Homelab Automations

1. **Media Management**:
   - Monitor Jellyfin for new additions
   - Trigger notifications
   - Organize library
   - Generate thumbnails

2. **Infrastructure**:
   - Provision VMs via Binary Lane CLI
   - Deploy Tailscale nodes
   - Monitor resource usage
   - Send alerts

3. **Data Workflows**:
   - Extract data from APIs
   - Transform and aggregate
   - Store in databases
   - Generate reports

4. **Content Pipeline**:
   - Monitor sources for new content
   - Process and organize
   - Route to appropriate services
   - Notify when ready

5. **System Integration**:
   - Sync data between services
   - Consolidate information
   - Create unified dashboards
   - Implement business logic

## Comparison with Alternatives

| Platform | Self-Hosted | Visual | Integrations | Pricing |
|----------|------------|--------|--------------|----------|
| **n8n** | Yes | Yes | 400+ | Open-source |
| **Make (Zapier-like)** | No (Cloud) | Yes | 1000+ | Freemium |
| **Airflow** | Yes | CLI-focused | Extensive | Open-source |
| **Temporal** | Yes | Limited | Custom | Open-source |

## Relevant Resources

- [n8n-io/n8n](https://github.com/n8n-io/n8n) — Official repository
- [n8n Documentation](https://docs.n8n.io) — Official docs
- [n8n Community](https://community.n8n.io) — Community forum
- [n8n Workflows](https://n8n.io/workflows) — Community workflows
- Related topics: [[Proxmox VE Homelab Management]], [[Open-WebUI]], [[Hermes Multi-Agent Workflow]], [[Automation]]

## Deployment Architecture

### Basic Setup

```
Proxmox VE
└── n8n Container/VM
    ├── Web Interface (port 5678)
    ├── Workflow Engine
    ├── Database (SQLite/PostgreSQL)
    └── Credentials Vault
```

### Advanced Setup

```
Proxmox VE
├── n8n Main (orchestrator)
├── n8n Worker (execution)
├── n8n Worker (execution)
└── PostgreSQL (shared database)
```

## Workflow Building Blocks

### Node Types

1. **Trigger Nodes**: Start workflow (webhook, schedule, manual)
2. **Action Nodes**: Do something (HTTP request, send email, etc.)
3. **Logic Nodes**: Conditional branching and loops
4. **Transform Nodes**: Manipulate data
5. **Integration Nodes**: Pre-built connectors

### Example Workflow Structure

```
Trigger (Webhook received)
  ↓
Fetch data from API
  ↓
Transform data
  ↓
Conditional: Valid data?
  ├─ Yes → Store in database
  │         └─ Send notification
  └─ No → Log error
  ↓
End
```

## Setup & Installation

### Docker Deployment

```bash
docker run -it --rm \
  --publish 5678:5678 \
  --env N8N_BASIC_AUTH_ACTIVE=true \
  --env N8N_BASIC_AUTH_USER=admin \
  --env N8N_BASIC_AUTH_PASSWORD=changeme \
  docker.io/n8nio/n8n
```

### Proxmox LXC

- [ ] Create LXC container
- [ ] Install Node.js runtime
- [ ] Deploy n8n package
- [ ] Configure database
- [ ] Set up reverse proxy
- [ ] Secure with TLS

## Integration Examples

### Available Connectors

- **APIs**: HTTP requests to any REST API
- **Databases**: PostgreSQL, MySQL, MongoDB
- **Cloud Services**: AWS, Google Cloud, Azure
- **Communication**: Email, Slack, Discord, Telegram
- **Webhooks**: Trigger from external sources
- **Scheduling**: Cron-based triggers
- **Custom Code**: JavaScript/Python

### Example Integrations

1. **Jellyfin + Notifications**:
   - Monitor Jellyfin for new items
   - Send Telegram notification
   - Update Kavita with new comics

2. **Binary Lane + Tailscale**:
   - Receive request to provision node
   - Create VM via Binary Lane API
   - Generate Ignition config
   - Deploy and join Tailnet

3. **Data Aggregation**:
   - Fetch from multiple APIs
   - Combine and transform
   - Store in database
   - Generate reports

## Learning Path

1. **Platform Familiarization**:
   - [ ] Install n8n locally
   - [ ] Build simple workflow
   - [ ] Explore node library
   - [ ] Review documentation

2. **Integration Discovery**:
   - [ ] List available connectors
   - [ ] Test API integrations
   - [ ] Set up credentials
   - [ ] Test error handling

3. **Use Case Design**:
   - [ ] Identify first automation
   - [ ] Map workflow steps
   - [ ] Design data flows
   - [ ] Plan error scenarios

4. **Implementation**:
   - [ ] Build workflow
   - [ ] Test with real data
   - [ ] Add error handling
   - [ ] Schedule execution
   - [ ] Monitor performance

5. **Scaling**:
   - [ ] Deploy to Proxmox
   - [ ] Set up database
   - [ ] Configure workers (if needed)
   - [ ] Document workflows
   - [ ] Train on usage

## Technical Considerations

**Scalability**: Single instance handles hundreds of workflows. Workers available for horizontal scaling.

**Data Storage**: SQLite suitable for testing, PostgreSQL for production.

**Credentials**: All secrets encrypted at rest and in transit. Separate credential vault.

**Error Handling**: Comprehensive error handling with retries, delays, and error branches.

**Monitoring**: Built-in logging and error tracking. Integration with external monitoring tools.

## Cost-Benefit Analysis

**Benefits**:
- No-code automation (fast to build)
- Self-hosted (no cloud costs)
- Extensive integrations
- Visual workflow builder
- Active community

**Costs**:
- Infrastructure resources
- Learning curve
- Maintenance and monitoring
- Custom logic may require coding

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*