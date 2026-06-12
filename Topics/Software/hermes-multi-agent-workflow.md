# Hermes Multi-Agent Workflow Framework

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Active  
**Tags**: agentic-systems, multi-agent, workflow-orchestration, triage-pipeline, task-routing

## Overview

Hermes Multi-Agent Workflow is a reusable skeleton for autonomous multi-agent triage pipelines built on the Hermes agent platform. Provides a complete working framework for detecting, deduplicating, scoring, researching, routing, and fulfilling items through parallel agent workflows with human approval gates.

## Key Points

- **Complete Pipeline**: Sources → Intake → Dedup → Score → Research (parallel) → Route → Paths → Human Gate → Fulfill → Deliver
- **Kanban-Based**: Hermes Kanban board as message bus and coordination layer
- **Domain-Agnostic Engine**: Generic deterministic engine; all domain logic in single YAML config
- **Flexible Routing**: Multiple fulfillment paths with automatic routing based on scoring rubric
- **Human-in-Loop**: Single approval gate with modify/approve/shelve options
- **Research Parallelization**: Multi-lane research for comprehensive coverage
- **Self-Improving**: Retrospective learning captures failures and improves harness

## Pipeline Stages

### Data Flow

```
sources → intake → dedup → score → research (parallel) → route
                                                            │
                   ┌──────────────┬──────────────────────┬─┤
                 path A           path B                shelve
                (prep)           (prep)                (auto)
                   └──────┬───────┘
                    ── HUMAN GATE ──   approve · shelve · modify
                   ┌──────┴───────┐
                 fulfill        fulfill
                   └──────┬───────┘
                       deliver
```

### Reference Implementation

Includes worked example for AI-agent pain points:
- **Scouts**: Watch X/Grok, Reddit, YouTube, web for user pain points
- **Rubric**: Score frequency, intensity, solvability, solution gap, strategic fit
- **Research**: Verify sources, gather context, audit solutions
- **Route**: `missing`/`broken` → build; `confusing`/`underdocumented` → video; `good` → shelve
- **Gate**: Telegram approval per item
- **Paths**: Build path (prototype → test → report), Video path (slides → script → deliver)

## Problem/Motivation

Want to explore agentic systems and workflow orchestration for future automation projects. Hermes provides proven pattern for multi-agent coordination that could apply to homelab infrastructure management, content curation, or other domains. Complements [[Pi.dev - Agentic Framework & Software]] and [[Case - Agentic PR Reliability]] for comprehensive agentic tooling.

## Relevant Resources

- [tonbistudio/hermes-multi-agent-workflow](https://github.com/tonbistudio/hermes-multi-agent-workflow) — Official repository
- [Hermes Platform](https://github.com/NousResearch/hermes-agent) — Underlying agent framework
- Related topics: [[Pi.dev - Agentic Framework & Software]], [[Case - Agentic PR Reliability]], [[Agentic Systems]]

## Adaptation Framework

### Core Customization

1. **Edit `triage.yaml`**: Sources, rubric, research lanes, route map, paths, roles
2. **Edit `paths/` templates**: Scope rails, deliverable specs, proposal formats
3. **Edit `skills/templates/`**: Scout queries, orchestrator notes
4. **Keep `engine/` generic**: Domain-agnostic logic stays unchanged

### Reusable Patterns

- **GitHub issue triage**: Repo issues → dedup → score (severity/frequency) → route (bug/docs/wontfix)
- **Sales lead triage**: Forms → score (fit/intent/budget) → route (qualified/nurture/junk)
- **Support tickets**: Queue → score (severity/SLA) → route (known/bug/clarify)
- **Content moderation**: Reports → verify → classify → action

## Learning & Exploration

- [ ] Review architecture and pipeline stages documentation
- [ ] Study reference implementation for AI-agent pain points
- [ ] Run unit tests and validate example config
- [ ] Design domain-specific triage for personal project
- [ ] Set up Hermes platform and profiles
- [ ] Implement scouts and fulfillment paths
- [ ] Deploy with human approval gate
- [ ] Iterate on rubric and routing logic

## Technical Notes

**Configuration**: Entire pipeline defined in `triage.yaml` with supporting markdown templates. Single source of truth for all routing, scoring, and fulfillment logic.

**Security**: Runs LLM-authored code behind human gate. Read SECURITY.md before deployment. Include secret-scan checklist before open-sourcing adapted copy.

**Testing**: Generic engine tests stay green. Domain tests in `tests/` validate example. Keep engine tests passing when adapting to new domain.

**Self-Improvement**: Retrospective agent captures learnings under `.case/learnings.md` and proposes harness improvements under `.case/amendments/`. Escalates repeated failures into docs, playbooks, or enforcement.

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*