# Open-WebUI - Local LLM Interface

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Active  
**Tags**: llm-interface, local-ai, open-source, web-ui, self-hosted

## Overview

Open-WebUI is a self-hosted, open-source LLM interface for running and managing local language models. Currently deployed in homelab but credentials need recovery.

## Current Status

### Existing Deployment

- **Status**: Hosted on Proxmox VE infrastructure
- **Credentials**: Lost/forgotten (but can reset via VM/LXC access)
- **GPU Passthrough**: Future consideration for inference acceleration

### Immediate Actions

- [ ] Access Proxmox console
- [ ] Locate Open-WebUI container/VM
- [ ] Reset admin credentials
- [ ] Document new credentials securely
- [ ] Test basic functionality

## Future Plans

### GPU Acceleration

**Goal**: Passthrough Intel GPU for local LLM inference

1. **Hardware Assessment**:
   - [ ] Identify Intel GPU in host system
   - [ ] Check Proxmox GPU passthrough support
   - [ ] Verify driver availability

2. **Configuration**:
   - [ ] Enable IOMMU in BIOS
   - [ ] Configure Proxmox PCI passthrough
   - [ ] Install GPU drivers in container
   - [ ] Benchmark inference speed

3. **Model Selection**:
   - [ ] Quantized models (Q4, Q5, Q8)
   - [ ] Memory requirements
   - [ ] Inference speed expectations
   - [ ] Local vs remote model storage

### Integration Points

- **Integration with Terax**: AI panel in terminal IDE
- **Integration with n8n**: Automation workflows
- **Integration with Free Claude Code**: Fallback LLM option
- **Agentic Workflows**: Custom agents and tools

## Relevant Resources

- [open-webui/open-webui](https://github.com/open-webui/open-webui) — Official repository
- [Ollama](https://ollama.ai) — Local model runner
- [LM Studio](https://lmstudio.ai) — Alternative UI
- Related topics: [[Terax AI Terminal]], [[Free Claude Code]], [[n8n Automation]], [[Agentic Systems]]

## Supported Models

### Popular Options

- **Llama 2**: Meta's open model
- **Mistral**: Efficient small models
- **Neural Chat**: Intel-optimized
- **Dolphin**: Uncensored variants
- **Wizardlm**: Instruction-tuned

### Quantization Levels

| Level | VRAM Needed | Speed | Quality |
|-------|-------------|-------|----------|
| Q4 | 4-8 GB | Fast | Good |
| Q5 | 8-12 GB | Medium | Very Good |
| Q8 | 16+ GB | Slow | Excellent |

## Deployment Architecture

### Current Setup

```
Proxmox VE
└── Open-WebUI Container/VM
    ├── Web Interface (port 8080)
    ├── Model Storage
    └── Database
```

### Future GPU-Accelerated Setup

```
Proxmox VE
└── Open-WebUI Container/VM
    ├── Web Interface
    ├── Ollama/LM Studio (GPU-accelerated)
    ├── Model Storage
    └── Database
    └── Intel GPU (passthrough)
```

## Setup & Configuration

### Credential Recovery

```bash
# SSH into Proxmox host
ssh root@proxmox-host

# Access the container
pct exec <container-id> bash

# Reset admin password (exact command depends on Open-WebUI version)
# Usually involves database reset or admin command
```

### Model Management

1. **Pull Models**:
   - Use Open-WebUI UI to download models
   - Or use Ollama CLI directly

2. **Configure Quantization**:
   - Select appropriate GGUF quantization
   - Consider VRAM constraints
   - Test inference latency

3. **Performance Tuning**:
   - Adjust context window size
   - Set batch size
   - Configure GPU memory allocation
   - Monitor thermal and power

## Learning Path

1. **Credential Recovery**:
   - [ ] Access Proxmox console
   - [ ] Locate Open-WebUI installation
   - [ ] Reset admin credentials
   - [ ] Update password manager

2. **GPU Passthrough Setup** (future):
   - [ ] Research Intel GPU passthrough on Proxmox
   - [ ] Test with small quantized model
   - [ ] Benchmark performance gain
   - [ ] Document configuration

3. **Model Selection & Testing**:
   - [ ] Try different models
   - [ ] Evaluate quality vs speed
   - [ ] Find optimal settings
   - [ ] Create prompt library

4. **Integration**:
   - [ ] Connect with Terax terminal
   - [ ] Test with n8n workflows
   - [ ] Consider Free Claude Code fallback
   - [ ] Build custom agents

## Cost Considerations

**Advantage over Cloud LLMs**:
- No per-token costs
- Privacy (no data sent to cloud)
- Unlimited inference
- Control over model selection

**Trade-offs**:
- Hardware investment (GPU)
- Power consumption
- Setup complexity
- Slower inference (vs cloud GPUs)

## Technical Notes

**Context Window**: Larger windows consume more VRAM. Typical range 2k-8k tokens.

**Batch Size**: Trade-off between throughput and memory usage.

**Temperature/Top-P**: Parameters for response randomness.

**System Prompts**: Can prime models for specific tasks (coding, writing, analysis).

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*