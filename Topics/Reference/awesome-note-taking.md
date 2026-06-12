# Awesome Note-Taking Curated Resources

**Category**: Reference  
**Added**: 2026-06-12  
**Status**: Reference  
**Tags**: note-taking, personal-knowledge-management, tools-comparison, pkm, documentation

## Overview

"Awesome Note-Taking" is a curated list of note-taking applications, tools, and resources. Provides comprehensive comparison of options from simple note apps to full personal knowledge management systems.

## Problem/Motivation

Considering options for note-taking and personal knowledge management. Obsidian is a strong candidate. This curated list provides context for evaluating alternatives and understanding the landscape of available tools.

## Note-Taking Tool Categories

### Simple Notes
- **Apple Notes**: Built-in, minimal features
- **Google Keep**: Cloud-based, sync across devices
- **Standard Notes**: Encrypted, minimal

### Rich Text Editors
- **Notion**: All-in-one workspace
- **OneNote**: Microsoft's note app
- **Evernote**: Established, feature-rich

### Markdown-Based
- **Obsidian**: Local-first, powerful linking
- **LogSeq**: Outliner with backlinking
- **Zettlekasten**: Cards and connections

### Knowledge Management
- **Roam Research**: Networked thought
- **Athens Research**: Open-source Roam
- **TiddlyWiki**: Personal wiki

### Wiki/Documentation
- **MediaWiki**: Wikipedia engine
- **DokuWiki**: Simple wiki
- **GitBook**: Documentation platform

## Obsidian Assessment

**Why Obsidian**:
1. **Local-First**: Files stored locally, not cloud
2. **Markdown**: Open format (future-proof)
3. **Linking**: Powerful backlinks and network views
4. **Plugins**: Extensive plugin ecosystem
5. **Community**: Large and active community
6. **Privacy**: No telemetry or cloud required
7. **Cross-Platform**: Windows, Mac, Linux, iOS, Android

**Potential Concerns**:
- Closed-source core
- Learning curve for advanced features
- Plugin ecosystem quality varies
- Mobile app requires paid subscription for sync

## Integration Ideas

### With Research Repository

- Use Obsidian to maintain this research repository
- Leverage linking to connect topics
- Generate knowledge graph visualization
- Export to HTML for sharing

### With Homelab

- Document infrastructure
- Maintain runbooks
- Store configuration notes
- Link to resources and guides

### With Development

- Project notes and design documents
- Learning logs and insights
- Code snippets and examples
- Architecture diagrams

## Relevant Resources

- [tehtbl/awesome-note-taking](https://github.com/tehtbl/awesome-note-taking) — Curated list
- [Obsidian.md](https://obsidian.md) — Local note app
- [Obsidian Vault Guide](https://help.obsidian.md/Obsidian) — Documentation
- [Obsidian Plugins](https://obsidian.md/plugins) — Plugin ecosystem
- Related topics: [[Personal Knowledge Management]], [[Documentation]], [[Research Tools]]

## Evaluation Criteria

### Essential Features

- [ ] Markdown support
- [ ] Linking and backlinking
- [ ] Search capability
- [ ] Export options
- [ ] Cross-platform support

### Nice-to-Have Features

- [ ] Knowledge graph visualization
- [ ] Mobile sync
- [ ] Plugin ecosystem
- [ ] Template system
- [ ] Version history

### Non-Negotiables

- [ ] Privacy/local storage
- [ ] Open format or export capability
- [ ] Reliability and stability
- [ ] Active maintenance
- [ ] Community support

## Implementation Plan

1. **Tool Selection**:
   - [ ] Review awesome-note-taking list
   - [ ] Short-list 3-5 candidates
   - [ ] Test with sample notes
   - [ ] Evaluate learning curve

2. **Obsidian Setup** (if selected):
   - [ ] Install Obsidian
   - [ ] Create vault for research repo
   - [ ] Configure plugins
   - [ ] Set up templates
   - [ ] Import existing notes

3. **Integration**:
   - [ ] Link to Topics structure
   - [ ] Create index and TOC
   - [ ] Set up daily notes
   - [ ] Configure search
   - [ ] Export workflows

4. **Maintenance**:
   - [ ] Regular backup to git
   - [ ] Monitor dead links
   - [ ] Refine categories
   - [ ] Archive outdated notes

## Technical Considerations

**Storage**: Obsidian vaults are just folders of markdown files - can be synced with git.

**Linking**: Obsidian links are plain markdown `[[note]]` format - readable in any editor.

**Plugins**: Popular plugins include:
- Dataview: Database queries on metadata
- Graph Analysis: Network visualization
- Daily Notes: Journaling template
- Calendar: Date-based navigation
- Templater: Dynamic templates

**Sync Options**:
- Git-based sync (free, manual)
- Obsidian Sync (paid cloud)
- Syncthing (free, background sync)
- Third-party cloud (Dropbox, OneDrive)

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*