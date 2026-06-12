# Research Repository

A portable, searchable research collection for software, hardware, car, house, and tech projects. Structured as Markdown files for maximum compatibility with external tools (Obsidian, Notion, LogSeq, etc.) and future expansion.

## Principles

- **KISS**: Keep It Simple, Structured — bullet points as baseline, expand where needed
- **Portable**: Plain Markdown files work anywhere
- **Linked**: Cross-references between topics enable discovery
- **Descriptive**: Enough context to kickstart projects months later
- **Agentic**: Consistent structure supports automated processing and agent workflows

## Directory Structure

```
research/
├── README.md (this file)
├── AGENTIC_NOTES.md (working patterns for this repo)
├── Topics/
│   ├── Software/
│   ├── Hardware/
│   ├── Home/
│   ├── Automotive/
│   └── General/
├── Resources/
│   └── Links.md (centralized link repository)
└── Projects/
    └── README.md (tracks active/planned projects)
```

## Quick Start

1. **Add a new research topic**: Create a `.md` file in `Topics/<Category>/`
2. **Store links**: Add to `Resources/Links.md` or embed in topic files
3. **Cross-reference**: Use `[[filename]]` wiki links for navigation
4. **Track projects**: Reference relevant topics in `Projects/README.md`

## File Template

See `TOPIC_TEMPLATE.md` for the standard format.

## Usage in External Tools

- **Obsidian**: Open the `research/` folder as a vault
- **Notion**: Import Markdown files
- **LogSeq**: Use as a knowledge base
- **Version Control**: Commit research progress to git
