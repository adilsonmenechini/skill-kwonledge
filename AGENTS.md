# AGENTS.md - Skill Kwonledge

## Project Overview

This is a **knowledge base repository** containing Obsidian-style knowledge notes and skills for managing them.

## Repository Structure

```
skill-kwonledge/
├── skills/              # OpenCode skills
│   ├── knowledge-manager/   # Unified skill (create + refactor)
│   ├── knowledge-creator/  # Create notes only
│   └── knowledge-refactor/ # Refactor only
├── skills-bkp/         # Backup of original skills
├── examples/          # Knowledge base
│   └── knowledge/
│       ├── kubernetes/
│       ├── terraform/
│       └── argocd/
└── .gitignore
```

## Primary Skill: knowledge-manager

This is the main skill to use for knowledge management.

### Trigger Phrases

**CREATE Mode:**
- "add [topic]" - add kubernetes, add docker, etc.
- "document [subject]"
- "create knowledge"
- "research [topic]"

**REFACTOR Mode:**
- "find duplicates"
- "merge notes"
- "clean up"
- "deduplicate"

### Usage

When user wants to add knowledge about a topic:

```bash
# Creates structure like:
knowledge/<topic>/
├── concepts/       # Explanatory content
├── guides/       # How-to content
├── references/   # Quick references/commands
└── INDEX.md    # Category index
```

## Knowledge Note Structure

Each note has:
- Frontmatter: `type`, `category`, `tags`, `status`, `created`
- Sections: Overview, Purpose, Content, Usage, Relationships, Notes, References
- [[Wiki-style links]] to related notes

## Available Knowledge Topics

- **Kubernetes**: architecture, pods, deployments, services, configmaps, ingress, helm
- **Terraform**: architecture, basics, commands
- **ArgoCD**: architecture, basics, commands

## Adding New Topics

1. Use the `knowledge-manager` skill
2. Request: "add [topic name]"
3. Skill creates folder structure automatically

Example: `add docker` → creates `knowledge/docker/` with concepts/, guides/, references/

## Tips for Agents

- Always use wiki-style links: `[[topic-name]]`
- Group notes by type: concepts/, guides/, references/
- Include practical examples in Usage sections
- Update INDEX.md after adding new notes
- NEVER leave empty sections in notes

## Conventions

- Category folder = topic name (lowercase, hyphen-separated)
- File path: `knowledge/<category>/<type>/<slug>.md`
- Frontmatter: type, category, tags, status, created (date)
- Use triggers from skill description to activate knowledge-manager