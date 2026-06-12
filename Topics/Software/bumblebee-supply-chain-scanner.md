# Bumblebee - Supply-Chain Compromise Scanner

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Active  
**Tags**: supply-chain-security, inventory-scanning, package-management, malware-detection, developer-security, sbom

## Overview

Bumblebee is a read-only inventory collector and supply-chain compromise scanner for macOS and Linux developer endpoints. Built by Perplexity AI, it detects when advisory-named packages, extensions, or versions match against developer machine local state.

## Key Points

- **Local Supply-Chain Response**: Scans lockfiles, package-manager metadata, extension manifests, and MCP configs
- **Read-Only Scanner**: No package manager execution, no source-file reads, no network calls during scan
- **Zero Dependencies**: Single static Go binary (1.25+), zero non-stdlib dependencies
- **Structured Output**: NDJSON format for integration with security workflows
- **Multi-Ecosystem**: Covers npm, pnpm, Yarn, Bun, PyPI, Go, RubyGems, Composer, MCP, agent skills, editor extensions, browser extensions, Homebrew
- **Threat Intel Integration**: Built-in exposure catalogs for recent supply-chain campaigns

## Problem/Motivation

Fills a critical gap in supply-chain incident response:
- **SBOMs** answer "what shipped"
- **EDR** answers "what ran or touched the network"
- **Bumblebee** answers "which developer machines have the compromised package right now?"

Useful for rapid exposure checks when responders already know what they're looking for.

## Technical Details

### Scan Profiles

| Profile | Use Case |
|---------|----------|
| `baseline` | Recurring lightweight inventory of global/user package roots, toolchains, extensions |
| `project` | Recurring inventory for known development directories (~/code, ~/src, ~/work) |
| `deep` | On-demand incident/campaign checks across explicit paths including home directory |

### Supported Ecosystems

- **JavaScript**: npm, pnpm, Yarn, Bun
- **Python**: PyPI
- **Go**: go modules
- **Ruby**: RubyGems
- **PHP**: Composer/Packagist
- **MCP**: Claude desktop and MCP configs
- **Agent Skills**: Vercel Labs skills
- **Extensions**: VS Code, Cursor, Windsurf, VSCodium, Firefox, Chromium browsers
- **Package Managers**: Homebrew

### Output Format

- **Package Records**: Full inventory of discovered packages with source metadata
- **Finding Records**: Exposure-catalog matches with severity and evidence
- **Confidence Levels**: high/medium/low based on metadata reliability

## Relevant Resources

- [perplexityai/bumblebee](https://github.com/perplexityai/bumblebee) — Official repository
- [Threat Intel Catalogs](https://github.com/perplexityai/bumblebee/tree/main/threat_intel) — Maintained exposure catalogs
- [Perplexity Computer](https://www.perplexity.ai/computer) — Threat intelligence source
- Related topics: [[Pi.dev - Agentic Framework & Software]], [[Supply-Chain Security]]

## Evaluation & Integration

- [ ] Review threat intelligence catalogs
- [ ] Evaluate for homelab deployment
- [ ] Test against local developer machines
- [ ] Integrate with security monitoring workflows
- [ ] Generate baseline inventory
- [ ] Set up incident response process

## Threat Intelligence Catalogs

Maintained exposure catalogs for recent campaigns:
- Mini/Shai-Hulud (npm/PyPI compromise)
- Laravel Lang (Composer compromise)
- Nx Console VS Code extension
- AntV/Mini Shai-Hulud worm wave
- node-ipc credential stealer
- GemStuffer (RubyGems)
- GlassWorm (IDE extension worm)
- TrapDoor Crypto Stealer (npm/PyPI/Cargo)

## Interesting Integration Points

- **Agentic Response**: Could integrate with [[Pi.dev - Agentic Framework & Software]] for automated incident response
- **Homelab Monitoring**: Add to [[Proxmox VE Homelab Management]] for fleet-wide inventory
- **CI/CD Integration**: Scan as part of development workflow

## Notes

Excellent tool for understanding local supply-chain exposure across development environments. Read-only nature makes it safe for continuous scanning. Built-in threat intel catalogs provide actionable starting point. Zero dependencies and single binary distribution make deployment straightforward.

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*
