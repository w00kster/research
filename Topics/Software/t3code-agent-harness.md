# T3 Code - Agent Harness Control Surface

**Category**: Software  
**Added**: 2026-10-21  
**Status**: Active  
**Tags**: agentic-systems, agent-harness, developer-tools, coding-agents, remote-control

## Overview

T3 Code is an "agent harness control surface" for managing AI coding agents from a mobile app, web app, or desktop client. It connects to local agent runtimes like Claude Code, Codex, Cursor, Grok Build, OpenCode, and Antigravity, making it a strong example of modern agent orchestration for developer workflows.

## Key Points

- **Remote control plane**: Manage agents from a phone, browser, or desktop instead of only a local terminal
- **Multi-provider support**: Works with Claude Code, Codex, Cursor, Grok Build, OpenCode, and Antigravity
- **Native Tailscale support**: The hosted web app appears to include a built-in connect flow for a tailnet, with CLI guidance to run the service with `--tailscale`
- **Local-first architecture**: Runs as a local web app and service with remote access options for mobile or other machines
- **Developer workflow focus**: Built around coding agents rather than a generic chat-only interface
- **Open control surface**: Framed as a flexible, forkable harness for agent-driven development

## Problem/Motivation

Interested in agentic work and harness patterns for coordinating local AI coding agents. T3 Code is relevant because it treats the experience as a control surface around multiple agent implementations, not just a single app wrapper. This sits directly alongside topics like [[Pi.dev - Agentic Framework & Software]], [[Omnigent - Meta-Harness AI Framework]], and [[Hermes Multi-Agent Workflow Framework]], and it complements the repo’s Tailscale networking work in [[Flatcar Ignition Generator with Tailscale]] and related homelab topics.

## Relevant Resources

- [pingdotgg/t3code](https://github.com/pingdotgg/t3code) — Official repository and project overview
- [T3 Code hosted web app](https://app.t3.codes/welcome) — Connect landing screen appears to expose native Tailscale/remote access patterns
- [T3 Code docs](https://github.com/pingdotgg/t3code/tree/main/docs) — Install, permissions, provider auth, and remote-access documentation
- [T3 Code install script](https://t3.codes/install.sh) — One-command install flow for the local service
- [LLM Bus](https://llm-bus.com/) — Shared-space coordination model for teams and AI agents; adjacent concept to a control-surface/harness pattern
- Related topics: [[Pi.dev - Agentic Framework & Software]], [[Omnigent - Meta-Harness AI Framework]], [[Hermes Multi-Agent Workflow Framework]], [[Turnstone - Agentic Development Framework]], [[Flatcar Ignition Generator with Tailscale]], [[Proxmox VE Homelab Management]]

## Next Steps

- [ ] Compare T3 Code with other agent harnesses and control surfaces
- [ ] Review docs covering permissions, providers, and remote access
- [ ] Evaluate how the harness pattern could fit into personal agent orchestration workflows

## Notes

T3 Code is still early-stage, but the design already makes a clear case for a remote-capable control plane around multiple agent providers. One notable detail is that the hosted experience appears to include native Tailscale support on the Connect landing modal, suggesting a first-class path for secure, networked access rather than a simple local-only web wrapper.

The CLI hints also reinforce this: `npx t3 pair` says to start T3 Code first, or run `npx t3 serve`; add `--tailscale` to use your tailnet. That signals intent for a managed, tailnet-aware remote workflow rather than a purely direct localhost-only setup.

The diagram from the earlier discussion is useful as a systems-level view of the same problem space: a shared operational context with chat, project memory, credentials, backups, GitHub, Tailscale networking, and agent execution all being treated as one coordinated system rather than isolated tools. That is conceptually similar to [LLM Bus](https://llm-bus.com/) and reinforces the idea that the valuable layer is not just the agent UI, but the shared state + routing + access model behind it.

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*
