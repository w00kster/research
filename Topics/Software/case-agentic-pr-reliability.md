# Case - Reliability Layer for Agent-Authored Pull Requests

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Active  
**Tags**: agentic-systems, pr-automation, agent-workflow, reliability, code-review, testing

## Overview

Case is the reliability layer for agent-authored pull requests. Its narrow job: turn a clearly scoped task into a reviewed PR with evidence, and make the next run better when this one fails. Not a generic platform or dashboard - a focused tool for making agent-authored code reliable and reviewable.

## Key Points

- **Narrow Focus**: PR loop reliability only - adjacent features revisited only after core is boring
- **Evidence Gates**: Tests, manual verification, code review, and PR creation all gated by evidence
- **Self-Improving**: Failures become docs, playbooks, and enforcement - harness learns from mistakes
- **Multi-Agent Pipeline**: Scout → Implementer → Verifier → Reviewer → Closer → Retrospective
- **Task-Based**: Clear task format separates human intent from machine-updated state
- **Isolated Responsibilities**: Each agent has focused, verifiable role
- **Context Isolation**: Scout context is read-only; structured findings synthesized by orchestrator

## Core Pipeline

```
scout → implementer → verifier → reviewer → closer → retrospective
```

### Agent Roles

| Agent | Responsibility | Does NOT Do |
|-------|-----------------|-------------|
| Orchestrator | Parse issues, create tasks, baseline check, dispatch pipeline | Implement code |
| Scout | Read-only exploration, structured findings | Edit code, write files |
| Implementer | Write fix, run tests, commit | Manual browser testing, PR creation |
| Verifier | Test user-facing scenario, record evidence | Edit code |
| Reviewer | Review diff against principles/conventions | Edit code or create PRs |
| Closer | Create PR after gates pass | Implement or test |
| Retrospective | Record learnings, propose improvements | Edit target repo code |

## Evidence Strategy

| Strategy | Evidence | Best For |
|----------|----------|----------|
| `ui-screenshot` | Playwright before/after screenshots | User-facing UI changes |
| `scenario-script` | Consumer script exercising scenario | Specific user workflows |
| `test-output` | Automated test output | Libraries, non-UI code |

## Problem/Motivation

Want to explore agentic systems and agent-authored code patterns for future automation. Case demonstrates production-grade approach to making agents reliable. Complements [[Pi.dev - Agentic Framework & Software]] and [[Hermes Multi-Agent Workflow Framework]] for comprehensive agentic tooling ecosystem.

## Relevant Resources

- [workos/case](https://github.com/workos/case) — Official repository
- Related topics: [[Pi.dev - Agentic Framework & Software]], [[Hermes Multi-Agent Workflow Framework]], [[Agentic Systems]]

## Task File Format

### Required Sections

```markdown
> **Mission**: What needs to happen and why
> **Repo**: Target repository path
> **Done when**: Acceptance criteria summary

# Title

## Objective
What needs to happen and why

## Target Repos
Which repos this touches

## Acceptance Criteria
- [ ] Checkbox items defining "done"

## Checklist
Step-by-step progress tracker

## Evidence Expectations
What proof of completion looks like

## Progress Log
Agent appends entries (never edit existing)
```

### Status Lifecycle

```
active → implementing → verifying/reviewing → closing → pr-opened → merged

Recovery:
  implementing → active
  verifying → implementing
  reviewing → verifying
  closing → verifying
```

## Learning & Exploration

- [ ] Review philosophy and core concepts
- [ ] Study multi-agent pipeline architecture
- [ ] Explore evidence gates and guardrails
- [ ] Review task file format and lifecycle
- [ ] Test with example target repo
- [ ] Design domain-specific task types
- [ ] Implement custom agents for specific workflows
- [ ] Build retrospective improvement loop

## Technical Notes

**Profiles**: `standard` (all phases) and `tiny` (skip verify for docs/typos/config)

**Revision Budget**: Default 2 cycles. Consecutive failures escalate to retrospective.

**Task Persistence**: Tasks live in `.case/tasks/active/` with markdown (human-readable) + JSON (machine-updated) companions.

**Embedded Assets**: Prompts, docs, playbooks, and AST rules bundled into standalone binary.

**Evidence Markers**: `.case/<task-slug>/tested`, `.case/<task-slug>/manual-tested`, `.case/<task-slug>/reviewed` files track evidence.

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*