# KeyLeak Detector - Runtime API Key & Secret Leak Detector

**Category**: Software  
**Added**: 2026-07-31  
**Status**: Active  
**Tags**: security, secrets, api-keys, baas, javascript, chrome-extension, vulnerability-scanning

## Overview

KeyLeak Detector is a runtime security tool that detects exposed API keys, secrets, and BaaS (Backend-as-a-Service) misconfigurations in web applications. Unlike static scanners that only find hardcoded secrets in source code, KeyLeak detects secrets that appear at runtime in JavaScript bundles, network requests, and DOM storage, then validates whether they're actually exploitable by testing associated services.

## Key Points

- **Runtime detection**: Finds secrets that only appear during runtime (not in static source)
- **BaaS vulnerability scanning**: Actively tests Supabase/Firebase/Appwrite configurations for misconfigurations (e.g., missing RLS rules)
- **JavaScript bundle analysis**: Scans minified/bundled JS for leaked keys and secrets
- **Chrome extension**: Provides real-time detection and validation while browsing
- **Active validation**: Tests discovered credentials to confirm if they're actually usable/exploitable
- **Multi-provider support**: Detects and validates keys for 15+ services (AWS, GitHub, Stripe, Firebase, Supabase, etc.)

## Problem/Motivation

Traditional secret scanning tools (like git-secrets, TruffleHog, etc.) only scan source code repositories and miss runtime leaks. Many web applications inadvertently expose API keys through client-side JavaScript, bundle analysis, or network traffic. Even when keys are found, determining if they're actually exploitable requires testing the associated services. KeyLeak bridges this gap by combining runtime detection with active validation.

## Relevant Resources

- [Amal-David/keyleak-detector](https://github.com/Amal-David/keyleak-detector) — Official repository
- Related topics: [[Web Security]], [[Secrets Management]], [[Vulnerability Scanning]], [[API Security]], [[Browser Extensions]]

## Next Steps

- [ ] Install and test the CLI tool
- [ ] Try the Chrome extension for real-time browsing protection
- [ ] Evaluate false positive/negative rates on test sites
- [ ] Assess performance impact on page load times
- [ ] Consider integration into CI/CD pipelines for pre-deployment scanning
- [ ] Research legal/ethical considerations for active validation of discovered credentials

## Notes

- Installation: `pip install keyleak-detector` or via UV
- CLI usage: `keyleak browser-scan https://example.com --html > report.html`
- Chrome extension available for real-time detection
- Includes subdomain enumeration via crt.sh, subfinder, amass
- Features 200+ domain suppression list to reduce false positives on common services (Google, AWS, Azure, GitHub, Stripe, etc.)
- Reports include per-source breakdown showing where each leak was found (JS, network, DOM, etc.)

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*