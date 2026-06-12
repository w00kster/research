# Stable Diffusion WebUI - Local Image Generation

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Backlog  
**Tags**: image-generation, ai-generation, stable-diffusion, local-gpu, computer-vision

## Overview

Stable Diffusion WebUI is the leading open-source interface for running Stable Diffusion locally. Enables text-to-image generation with full control and no cloud dependencies.

## Problem/Motivation

Interested in exploring local image generation capabilities. Could be cool to generate images locally with Intel GPU passthrough on a Proxmox node. Similar motivation to [[Open-WebUI]] but for visual content rather than text.

## Key Features

- **Text-to-Image**: Generate images from text descriptions
- **Image-to-Image**: Modify existing images
- **Inpainting**: Edit specific regions
- **LoRA Support**: Fine-tuned model adapters
- **Batch Processing**: Generate multiple images
- **Custom Models**: Community-created variants
- **Full Control**: Run entirely locally

## Current Interest Level

**Status**: Exploratory / Backlog
- Not immediate priority
- Would be "cool to have"
- Depends on GPU passthrough viability
- Potential for creative projects

## Hardware Requirements

### GPU Options

**Intel GPU**:
- [ ] Identify Intel iGPU or discrete GPU
- [ ] Check Proxmox passthrough support
- [ ] Assess VRAM allocation
- [ ] Test with small models

**Passthrough via Proxmox**:
- [ ] Enable IOMMU in BIOS
- [ ] Configure PCI passthrough
- [ ] Install drivers in container
- [ ] Benchmark performance

### Memory Requirements

| Model | VRAM | Notes |
|-------|------|-------|
| Stable Diffusion 1.5 | 4-6 GB | Quantized versions |
| Stable Diffusion XL | 8-12 GB | Better quality |
| ControlNet | +2-4 GB | Additional control |
| Custom LoRA | Minimal | Model adapters |

## Deployment Strategy

### Phase 1: Evaluation

- [ ] Research GPU passthrough on Proxmox
- [ ] Test basic setup without GPU
- [ ] Assess CPU-only inference speed
- [ ] Review model options

### Phase 2: GPU Integration (future)

- [ ] Identify Intel GPU to passthrough
- [ ] Configure Proxmox passthrough
- [ ] Install drivers
- [ ] Deploy Stable Diffusion
- [ ] Benchmark performance

### Phase 3: Advanced Features (if viable)

- [ ] Explore LoRA models
- [ ] Try ControlNet for composition control
- [ ] Batch generation workflows
- [ ] Integration with other tools

## Relevant Resources

- [AUTOMATIC1111/stable-diffusion-webui](https://github.com/AUTOMATIC1111/stable-diffusion-webui) — Official repository
- [Civitai](https://civitai.com) — Community models and LoRAs
- [Stable Diffusion Official](https://stability.ai) — Model source
- Related topics: [[Open-WebUI - Local LLM]], [[GPU Hardware]], [[Proxmox VE Homelab Management]]

## Model Options

### Base Models

- **Stable Diffusion 1.5**: Mature, many community models
- **Stable Diffusion XL**: Latest, higher quality
- **Dreamshaper**: Community favorite variant
- **Deliberate**: Anime-focused variant

### Extensions

- **ControlNet**: Composition control (poses, edges, etc.)
- **LoRA Models**: Specific styles or subjects
- **VAE**: Alternative decoders for quality
- **Samplers**: Different diffusion algorithms

## Use Cases

1. **Creative Exploration**: Generate concept art
2. **Illustration**: Create custom artwork
3. **Design Assets**: Generate textures, backgrounds
4. **Educational**: Learn about diffusion models
5. **Experimentation**: Test prompts and techniques

## Integration Ideas

- **Jellyfin**: Generate custom cover art
- **n8n**: Automated image generation workflows
- **Terax**: Image generation in terminal IDE
- **Web Preview**: Generate website mockups

## Learning Path

1. **GPU Assessment**:
   - [ ] Identify available GPU hardware
   - [ ] Research Proxmox passthrough process
   - [ ] Test basic passthrough setup

2. **Software Setup** (if GPU available):
   - [ ] Deploy Stable Diffusion WebUI
   - [ ] Download base model
   - [ ] Test inference
   - [ ] Benchmark performance

3. **Model Exploration**:
   - [ ] Try different base models
   - [ ] Experiment with LoRA adapters
   - [ ] Learn prompt engineering
   - [ ] Build prompt library

4. **Advanced Features**:
   - [ ] ControlNet setup and use
   - [ ] Batch generation
   - [ ] Fine-tuning for specific styles
   - [ ] Integration with other tools

## Technical Considerations

**Prompt Engineering**: Quality of prompts greatly affects output. Specificity matters (e.g., "oil painting" vs "digital art").

**Sampling Steps**: More steps = better quality but slower. Typical: 20-50 steps.

**Guidance Scale**: Higher values more closely follow prompt. Range: 7-15 typical.

**Seed**: Fixed seed reproduces exact results. Useful for iterations.

**Inference Speed**: CPU-only very slow. GPU acceleration critical for usability.

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*