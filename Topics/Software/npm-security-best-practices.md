# npm Security Best Practices

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Reference  
**Tags**: supply-chain-security, npm, package-management, developer-security, dependency-security

## Overview

Awesome npm Security Best Practices is a curated and practical list of security best practices for using npm packages. Covers safe-by-default package manager options, hardening against supply-chain attacks, deterministic dependency resolution, vulnerability scanning, and health signals.

## Scope

- Safe-by-default npm package manager command-line options
- Hardening against supply chain attacks
- Deterministic and secure dependency resolution
- Security vulnerabilities scanning and package health signals
- pnpm and bun package manager guidance where applicable

## Key Best Practices

### Disable Post-Install Scripts

**Critical**: Recent attacks (Shai-Hulud, Nx, event-stream) exploited npm postinstall scripts. Mitigate by disabling script execution.

```ini
# .npmrc
ignore-scripts=true
allow-git=none
min-release-age=30
```

**pnpm** (v10+): Disables postinstall by default. Use `allowBuilds` for exceptions:

```yaml
# pnpm-workspace.yaml
allowBuilds:
  esbuild: true
  rolldown: true
strictDepBuilds: true
blockExoticSubdeps: true
```

### Block Git-Based Dependencies

Reject `git+ssh://` and exotic subdependencies. Use `allow-git=none` in npm.

### Install with Cooldown

Block packages newer than 30 days (`min-release-age=30`). Allows time for vulnerability discovery before adoption.

### Hardening Tools

- **npq**: Hardens package installs with real-time scanning
- **Socket Firewall (sfw)**: Blocks known malicious packages
- **Snyk**: Automated dependency upgrades with cooldown
- **Dependabot**: GitHub-native dependency management
- **Renovate**: Advanced bot with customizable rules

### Prevent Lockfile Injection

Use `npm ci` (clean install) in CI/CD to prevent lockfile surprises.

### npm Maintainer Practices

1. Enable 2FA for npm accounts
2. Publish with Provenance Attestations
3. Publish with OIDC
4. Reduce dependency tree

### Package Health Signals

- Consult Snyk Security Database
- Don't trust official npmjs.org registry blindly
- Prevent dependency confusion attacks with private scopes

## Problem/Motivation

Future-proofing for potential npm adoption. Currently not using npm ecosystem, but this reference provides comprehensive security hardening checklist for when/if npm enters personal projects. Complements [[Bumblebee - Supply-Chain Compromise Scanner]] for runtime supply-chain protection.

## Relevant Resources

- [lirantal/npm-security-best-practices](https://github.com/lirantal/npm-security-best-practices) — Official repository
- [Snyk Security Database](https://snyk.io) — Vulnerability scanning
- [Socket Security](https://socket.dev) — Malicious package detection
- Related topics: [[Supply-Chain Security]], [[Bumblebee - Supply-Chain Compromise Scanner]], [[Dependency Management]]

## Reference Configuration

### npm (.npmrc)

```ini
# Disable lifecycle scripts
ignore-scripts=true

# Block git dependencies
allow-git=none

# 30-day cooldown
min-release-age=30
```

### pnpm (pnpm-workspace.yaml)

```yaml
# 30-day cooldown (43200 minutes)
minimumReleaseAge: 43200

# No trust regression
trustPolicy: no-downgrade

# Explicit build script allowlist
allowBuilds:
  esbuild: true
  rolldown: true
  unrs-resolver: true

# Enforce allowlist
strictDepBuilds: true

# Block git URLs
blockExoticSubdeps: true
```

## Implementation Checklist

- [ ] Review 17 best practices in depth
- [ ] Evaluate hardening tools (npq, Socket, Snyk)
- [ ] Understand dependency confusion attacks
- [ ] Prepare for CI/CD integration
- [ ] Document npm security policy
- [ ] Set up automated scanning
- [ ] Plan for supply-chain incident response

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*