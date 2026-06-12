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

## Future Agent Context

**This repo will benefit from automated workflows:**

- Detect broken links periodically
- Extract tags and generate topic indexes
- Identify orphaned topics (no backlinks)
- Cross-reference similar topics by title/tags
- Generate project readiness reports from topic coverage

**Preserve structure** to enable these workflows without manual intervention.
