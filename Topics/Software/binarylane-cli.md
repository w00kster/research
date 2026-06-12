# Binary Lane CLI - Infrastructure Provisioning Tool

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Active  
**Tags**: infrastructure, cloud-provisioning, cli-tools, vm-management, binary-lane

## Overview

Binary Lane CLI provides command-line interface for managing Binary Lane virtual machines and infrastructure. Complements [[Flatcar Ignition + Tailscale]] for programmatic VM provisioning and expansion of homelab infrastructure.

## Problem/Motivation

Currently has unused Binary Lane VMs (paid monthly) that could be leveraged for expanding homelab infrastructure. CLI tool enables automating VM provisioning, configuration, and lifecycle management via command-line.

## Key Features

- Programmatic VM management
- Infrastructure-as-code compatible
- Integration with Tailscale for networking
- Full API coverage via CLI
- Script automation capabilities

## Integration with Homelab

### Current Situation

- Existing Binary Lane VMs (underutilized, but paid)
- Proxmox VE as primary hypervisor
- Tailscale network backbone
- Growth opportunity for geographic distribution

### Proposed Workflows

1. **Automated Exit Node Deployment**:
   - Use Binary Lane CLI to provision VM
   - Generate Ignition config with Flatcar tool
   - Deploy Tailscale exit node automatically
   - Monitor via Pulse

2. **Failover/Redundancy**:
   - Provision standby nodes in different regions
   - Automatic failover using Tailscale routing
   - Cost-optimized resource allocation

3. **Burst Capacity**:
   - Spin up temporary nodes for compute-intensive tasks
   - Tear down after job completion
   - Pay-as-you-go expansion

## Relevant Resources

- [binarylane/binarylane-cli](https://github.com/binarylane/binarylane-cli) — Official repository
- [Binary Lane API Reference](https://api.binarylane.com.au/reference/) — Complete API documentation
- [Binary Lane Documentation](https://api.binarylane.com.au/) — General docs
- Related topics: [[Flatcar Ignition + Tailscale]], [[Proxmox VE Homelab Management]], [[Tailscale Networking]]

## Authentication & Setup

### API Key Management

- [ ] Generate API key from Binary Lane console
- [ ] Store in `.env` with proper permissions
- [ ] Set `BL_API_KEY` environment variable
- [ ] Test authentication with `bl auth test` or equivalent

### Installation

```bash
# Install Binary Lane CLI
git clone https://github.com/binarylane/binarylane-cli.git
cd binarylane-cli
# Install per repo instructions
```

## Learning Path

- [ ] Review CLI command documentation
- [ ] Study API reference for VM operations
- [ ] Test basic commands (list VMs, get info)
- [ ] Explore automation scenarios
- [ ] Design provisioning workflow
- [ ] Integrate with Flatcar tool
- [ ] Document cost tracking strategy

## Automation Ideas

### Script Examples

1. **Provision Tailscale Exit Node**:
   ```bash
   bl vm create --image flatcar --name exit-node-us
   # Generate Ignition config
   # Apply config to new VM
   # Join Tailnet
   ```

2. **List Existing Infrastructure**:
   ```bash
   bl vm list
   bl vm show <id>
   ```

3. **Cost Optimization**:
   - [ ] Monitor usage patterns
   - [ ] Identify unused resources
   - [ ] Schedule cleanup
   - [ ] Document cost baseline

## Cost Considerations

- **Current State**: Paying monthly for underutilized VMs
- **Opportunity**: Leverage them for expanded infrastructure
- **Risk**: Uncontrolled provisioning could increase costs
- **Mitigation**: Set monthly budgets, automate cleanup, regular audits

## Next Steps

1. **Assess Current Usage**:
   - [ ] List all Binary Lane VMs
   - [ ] Check last access date
   - [ ] Calculate current monthly spend
   - [ ] Plan reactivation strategy

2. **Pilot Deployment**:
   - [ ] Deploy test VM via CLI
   - [ ] Configure Tailscale integration
   - [ ] Validate networking
   - [ ] Document process

3. **Full Deployment**:
   - [ ] Provision geographic distributed nodes
   - [ ] Set up monitoring
   - [ ] Implement cost controls
   - [ ] Document architecture

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*