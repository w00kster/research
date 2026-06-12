# LTX-2 - Audio-Video Foundation Model

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Active  
**Tags**: video-generation, audio-video, ai-generation, diffusion, text-to-video, foundation-model

## Overview

LTX-2 is the first DiT-based (Diffusion Transformer) audio-video foundation model containing all core capabilities of modern video generation in one model: synchronized audio and video, high fidelity, multiple performance tiers, and advanced control via LoRA adapters.

## Key Points

- **Unified Audio-Video**: First model to jointly generate synchronized audio and video in single pass
- **DiT Architecture**: Asymmetric dual-stream diffusion transformer (14B video + 5B audio parameters)
- **Multiple Pipelines**: Text-to-video, image-to-video, video-to-video, audio-to-video, keyframe interpolation, lip dubbing
- **LoRA Control**: IC-LoRA for image/video conditioning, motion control, pose control, camera control, HDR output
- **Production Quality**: Two-stage pipelines for best quality (generation + 2x upsampling)
- **Performance Options**: Distilled model for fastest inference, FP8 quantization for memory efficiency
- **Advanced Features**: Automatic prompt enhancement, gradient estimation, lip-sync precision

## Core Capabilities

### Generation Modes

| Pipeline | Quality | Speed | Use Case |
|----------|---------|-------|----------|
| TI2VidTwoStagesPipeline | Highest | Medium | Production text/image-to-video (recommended) |
| TI2VidTwoStagesHQPipeline | Highest | Medium | Same as above, different sampler |
| DistilledPipeline | High | Fastest | Batch processing, speed critical |
| A2VidPipelineTwoStage | High | Medium | Audio-driven video generation |
| ICLoraPipeline | High | Medium | Video-to-video transformations |
| KeyframeInterpolationPipeline | High | Medium | Smooth animation between keyframes |
| LipDubPipeline | High | Medium | Lip dubbing with audio reference |
| RetakePipeline | Variable | Fast | Regenerate specific time regions |

### Model Components

- **Transformer**: Asymmetric dual-stream with bidirectional cross-modal attention
- **Video VAE**: Spatiotemporal compression with learnable latents
- **Audio VAE**: Spectrogram encoding with vocoder for waveform reconstruction
- **Text Encoder**: Gemma 3 multilingual with thinking tokens
- **Spatial Upscaler**: 2x resolution enhancement
- **Temporal Upscaler**: Frame interpolation capability

## Problem/Motivation

Interested in exploring audio/video generation for future projects. LTX-2 represents cutting-edge capabilities for creating synchronized media content. Could integrate with [[Supertonic TTS]] for audio-driven workflows, or use with [[Pi.dev - Agentic Framework & Software]] for agent-driven content generation.

## Relevant Resources

- [Lightricks/LTX-2](https://github.com/Lightricks/LTX-2) — Official repository
- [LTX.io](https://ltx.io) — Platform and demos
- [HuggingFace Models](https://huggingface.co/Lightricks/LTX-2.3) — Model checkpoints
- [Research Paper](https://arxiv.org/abs/2601.03233) — Architecture details
- Related topics: [[Supertonic TTS]], [[Media Generation]]

## Learning & Experimentation

- [ ] Review paper and architecture documentation
- [ ] Explore pipeline implementations and examples
- [ ] Test prompt engineering for video generation
- [ ] Evaluate LoRA adapter fine-tuning capabilities
- [ ] Assess memory/compute requirements on homelab infrastructure
- [ ] Experiment with audio-to-video for creative workflows
- [ ] Consider integration points with agentic systems

## Technical Notes

**Optimization Tips**:
- Use DistilledPipeline for fastest inference (8 steps stage 1, 4 steps stage 2)
- Enable FP8 quantization for reduced memory footprint
- Install FlashAttention 4 on Blackwell GPUs for optimal performance
- Use gradient estimation to reduce inference steps while maintaining quality
- Single-stage pipeline faster but lower resolution

**Prompting**: Detailed, chronological descriptions of actions and scenes work best. Include specific movements, appearances, camera angles, environmental details in single flowing prompt.

**Integration**: ComfyUI support available for node-based workflows. Python SDK and CLI for programmatic access.

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*