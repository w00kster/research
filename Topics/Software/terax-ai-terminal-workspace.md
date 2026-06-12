# Terax - AI-Native Terminal Workspace

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Active  
**Tags**: terminal, ai-native, developer-tools, workspace, code-editor, agentic-workflow

## Overview

Terax is a lightweight open-source terminal IDE built on Tauri 2 + Rust and React 19. Terminal-first application development environment with AI-native workflows, native PTY backend, WebGL renderer, and integrated agentic AI side-panel for multiple model providers.

## Key Features

### Terminal

- xterm.js with WebGL renderer for smooth rendering
- Multi-tab with background streaming
- Native PTY backend via `portable-pty` (zsh, bash, pwsh, fish, cmd)
- Split panels (horizontal and vertical)
- Inline search, link detection, true-color
- Per-tab workspace environments on Windows (Local or WSL distro)

### Code Editor

- CodeMirror 6 (TS/JS, Rust, Python, Go, C/C++, Java, HTML/CSS, JSON, Markdown, etc.)
- Inline AI autocomplete with local model support
- AI edit diffs - accept/reject hunk by hunk
- Vim mode
- 10 built-in editor themes (Atom One, Copilot, GitHub, Gruvbox, Nord, Tokyo Night, Xcode)

### Source Control

- Stage/unstage hunks, commit (Cmd+Enter / Ctrl+Enter)
- Branch display including detached HEAD
- Git history with real commit graph (lane rendering for merges)
- Commit search and filter

### File Explorer

- Catppuccin icon theme
- Fuzzy search, keyboard navigation, inline rename
- Attach files/selections to AI side-panel

### Web Preview

- Auto-detects local dev servers
- External URL preview via native child webview

### AI Workflows

- **Provider Support**: OpenAI, Anthropic, Google (Gemini), Groq, xAI (Grok), Cerebras, OpenRouter, DeepSeek, Mistral, OpenAI-compatible endpoints, plus local (LM Studio, MLX, Ollama)
- **Agentic**: Plans, sub-agents, project memory via `TERAX.md`, file operations, bash with approval gating
- **Composer**: Snippets via `#handle`, files via `@path`, slash commands, voice input
- **Custom Agents**: System prompt and tool subset per agent
- **Plan Mode**: Multi-step work with generation confirmation

## Problem/Motivation

Interested in AI-native development workflows and agentic systems integration. Terax represents modern approach to combining terminal, editor, and agentic AI in single environment. Could serve as frontend for homelab development or integration point for [[Pi.dev - Agentic Framework & Software]] and [[Case - Agentic PR Reliability]] workflows.

## Relevant Resources

- [crynta/terax-ai](https://github.com/crynta/terax-ai) — Official repository
- [Terax Website](https://terax.app) — Platform info
- [Terax Docs](https://terax.app/docs) — Documentation
- Related topics: [[Pi.dev - Agentic Framework & Software]], [[Development Tools]], [[AI-Native Development]]

## Technical Stack

- **Frontend**: React 19, TypeScript, Vite, Tailwind v4, shadcn/ui, Zustand
- **Backend**: Tauri 2, Rust, `portable-pty`, xterm.js, CodeMirror 6
- **AI**: Vercel AI SDK v6

## Build & Install

### From Releases

Latest installers available on [Releases](https://github.com/crynta/terax-ai/releases/latest). Auto-updates enabled.

### From Source

**Prerequisites**: Rust (stable), Node 20+, pnpm, Tauri prerequisites

```bash
pnpm install
pnpm tauri dev          # development
pnpm tauri build        # production bundle
```

### Type Checking

```bash
pnpm exec tsc --noEmit                          # frontend
cd src-tauri && cargo clippy --all-targets     # Rust
cd src-tauri && cargo test --locked            # tests
```

## Platform Notes

### Windows

- Not code-signed yet - Windows shows warning, click "Run anyway"
- Default shell: PowerShell 7+ → PowerShell 5.1 → cmd.exe
- WSL is first-class environment

### Linux

- **Arch/AUR**: `yay -S terax-bin`
- **AppImage**: Needs FUSE, or use `--appimage-extract-and-run`
- Wayland rendering glitches: try `WEBKIT_DISABLE_DMABUF_RENDERER=1`

## Integration Ideas

- **Local Development**: Replace traditional terminal + editor setup
- **Agent Orchestration**: Front-end for agentic workflows
- **Homelab Management**: SSH into homelab devices with integrated terminal
- **AI-Driven Development**: Leverage agentic mode for complex refactoring
- **Code Review**: Integrated diff viewing with AI commentary

## Learning Path

- [ ] Install and explore terminal/editor capabilities
- [ ] Configure AI provider and test workflows
- [ ] Experiment with agentic planning mode
- [ ] Build custom agent for domain-specific tasks
- [ ] Integrate with local model server (Ollama, LM Studio)
- [ ] Explore integration with homelab infrastructure

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*