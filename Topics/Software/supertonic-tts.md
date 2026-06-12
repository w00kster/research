# Supertonic - On-Device Multilingual TTS

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Active  
**Tags**: audio-synthesis, tts, text-to-speech, multilingual, edge-device, ai-audio

## Overview

Supertonic is a lightning-fast, on-device multilingual text-to-speech system built on ONNX Runtime. Designed for local inference with minimal overhead across desktop, browser, mobile, and edge devices. Runs entirely on device with no network dependency.

## Key Points

- **Blazingly Fast**: Low-latency, real-time synthesis - converts entire webpages to audio in under a second
- **31-Language Multilingual**: Direct synthesis across 31 languages, or language-agnostic mode
- **Compact Model**: 99M-parameter open-weight model (fraction the size of 0.7B-2B class systems)
- **Edge-Ready**: Runs locally on desktop, mobile, browsers, Raspberry Pi, e-readers - complete privacy
- **Studio Quality**: 44.1kHz 16-bit WAV output, production-ready without external upsampling
- **Expression Tags**: 10 inline tags (`<laugh>`, `<breath>`, `<sigh>`) for natural human nuance
- **Multi-Runtime**: ONNX Runtime SDKs for Python, Node.js, Browser (WebGPU), Java, C++, C#, Go, Swift, iOS, Rust, Flutter

## Supported Languages (31)

Arabic, Bulgarian, Croatian, Czech, Danish, Dutch, English, Estonian, Finnish, French, German, Greek, Hindi, Hungarian, Indonesian, Italian, Japanese, Korean, Latvian, Lithuanian, Malay, Norwegian, Polish, Portuguese, Romanian, Russian, Slovak, Spanish, Swedish, Turkish, Ukrainian

## Problem/Motivation

Want to explore audio/video generation capabilities for future projects. Supertonic could be integrated with [[Proxmox VE Homelab Management]] for audio-driven automation, or combined with [[LTX-2 Audio-Video Generation]] for synchronized audio-video workflows.

## Relevant Resources

- [supertone-inc/supertonic](https://github.com/supertone-inc/supertonic) — Official repository
- [Hugging Face Models](https://huggingface.co/Supertone/supertonic-3) — Pre-trained models
- [Voice Builder Demo](https://supertonic.supertone.ai/voice-builder) — Voice cloning
- Related topics: [[LTX-2 Audio-Video Generation]], [[Audio Processing]]

## Deployment & Integration

- [ ] Review ONNX Runtime implementations for target platform
- [ ] Test on homelab infrastructure
- [ ] Evaluate Python SDK for automation workflows
- [ ] Consider local HTTP server mode (`supertonic serve`) for agent integration
- [ ] Explore voice builder for custom voice profiles

## Technical Notes

**Local HTTP Server**: Python SDK can run as local HTTP service with native `/v1/tts` and OpenAI-compatible `/v1/audio/speech` endpoints - useful for local agents and browser extensions.

**Multi-Runtime Support**: Broad ecosystem of implementations enables deployment across diverse infrastructure from mobile to edge devices to desktop.

**Quality Spectrum**: 5-12 denoising steps for quality control, speed adjustable (0.7-2.0x), automatic text chunking for long-form synthesis.

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*