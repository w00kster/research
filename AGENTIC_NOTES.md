# Agentic Working Patterns

This document captures how we work within this repository to enable consistent agent-assisted expansion and future workflows.

## Working Principles for Agents

### When Adding Research Topics

1. **Examine existing structure** before creating new categories
2. **Use consistent metadata** at the top of each file:
   - `# Title` — clear, searchable heading
   - `Added: YYYY-MM-DD` — when created
   - `Status: [Active/Archived/Backlog]` — lifecycle indicator
   - `Tags: [tag1, tag2]` — for filtering and searching
3. **Organize by category first** (`Topics/<Category>/`)
4. **Cross-link aggressively** using wiki-style links: `[[filename]]` or `[[filename#section]]`
5. **Keep files focused** — one topic per file, link to related topics

### Structure for Scalability

- **Topics** are atomic research units (a project, a technology, a problem)
- **Categories** group topics (Software, Hardware, etc.)
- **Resources** are external references (links, references)
- **Projects** track active work pulling from Topics

### Information Density

- **Baseline**: Bullet points with brief descriptions
- **Expand as needed**: Add sections for deeper context, but prefer linking to related topics
- **Context**: Always include "why this matters" or use-case when not obvious

### Cross-Repository Workflow

When expanding this repo with new topics:

1. Check `Resources/Links.md` for existing references
2. Link to related topics in the same category
3. Add relevant tags for discoverability
4. If spawning a project: create entry in `Projects/README.md` referencing relevant topics

### Git Workflow

- Commit topic additions with descriptive messages: "Add: <topic name> in <category>"
- Batch URI research sessions into single commits: "Add: Research round - <date>"
- Tag milestones: `v1-initial-scaffold`, `research-<month>-<year>`

## Operational Guidelines for URI Processing (Updated 2026-06-12)

### No Confirmation Blocking

**Agent should write topics directly to the repository without requiring user confirmation prompts.** This prevents credit waste and keeps research momentum flowing. Only request confirmation in edge cases or when fundamental decisions cannot be made.

### Auto-Scan for Context

When processing URIs:
- Scan GitHub repositories to understand actual content and purpose
- Read READMEs, documentation, and key files to determine accurate categorization
- Extract relevant technical details for topic files
- Identify cross-topic connections and relationships

### Smart Categorization

Place topics in the most appropriate category based on actual content analysis:
- **Software**: Programming frameworks, tools, libraries, development utilities, supply-chain security, agentic systems
- **Hardware**: Physical infrastructure, homelab, devices, monitoring systems, Proxmox ecosystem
- **Automotive**: Vehicle-related projects, GPS tracking, transportation tech
- **Home**: Home automation, smart home, home infrastructure
- **General**: Cross-cutting, miscellaneous, foundational research

### Deferred Decisions

When confident categorization isn't possible:
- Create a pull request instead of making uncertain commits
- Include analysis and proposed category in PR description
- Let user review and decide final placement

### URI Batch Processing

When given a batch of URIs:
1. Process each independently without intermediate summaries
2. Scan for context if needed (read README, key files)
3. Determine correct category based on content
4. Create topic file with full details (metadata, overview, key points, resources, evaluation framework)
5. Commit directly without confirmation
6. Provide single summary of batch when complete

## Future Agent Context

**This repo will benefit from automated workflows:**

- Detect broken links periodically
- Extract tags and generate topic indexes
- Identify orphaned topics (no backlinks)
- Cross-reference similar topics by title/tags
- Generate project readiness reports from topic coverage
- Automated agentic response workflows using Pi.dev framework

**Preserve structure** to enable these workflows without manual intervention.
