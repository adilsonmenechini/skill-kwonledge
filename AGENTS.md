# AGENTS.md - Skill Kwonledge

## Project Overview

This is a **knowledge base repository** containing Obsidian-style knowledge notes and skills for managing them.

## Repository Structure

```
skill-kwonledge/
├── skills/              # OpenCode skills
│   ├── knowledge-manager/   # Unified skill (create + refactor)
│   ├── knowledge-creator/    # Create notes only
│   └── knowledge-refactor/     # Refactor only
├── examples/           # Knowledge base
│   └── knowledge/
│       ├── kubernetes/
│       ├── terraform/
│       ├── argocd/
│       └── INDEX.md
├── AGENTS.md           # Agent instructions (this file)
├── .gitignore
└── README.md
```

---

## Primary Skill: knowledge-manager

This is the main skill for knowledge management in this repo.

### Trigger Phrases

**CREATE Mode:**
- "add [topic]" - e.g., "add kubernetes", "add docker"
- "document [subject]"
- "create knowledge"
- "research [topic]"
- "learn about"

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
├── guides/         # How-to content
├── references/     # Quick references/commands
└── INDEX.md        # Category index
```

---

## Skill Anatomy Reference

For creating new skills in this repo, follow this pattern based on `skill-creator` framework:

### Basic Structure

```
skills/<skill-name>/
├── SKILL.md              # Main skill file (REQUIRED)
├── INDEX.md             # Skill description & examples
├── evals/
│   └── evals.json       # Test cases
└── resources/
    ├── template.md     # Output template
    └── quality_rules.md # Quality standards
```

### SKILL.md Required Elements

```yaml
---
name: <skill-name>
description: <detailed "pushy" description with triggers>
triggers: ["phrase1", "phrase2", "phrase3"]
tools: [filesystem, read, write]
category: <domain>
---

# <Skill Name>

## Purpose
<One sentence on what this skill does>

## When to use
- Trigger when user says X
- Trigger when user wants Y
- Also trigger when Z

## Instructions

### Step 1: <Action>
<Detailed instructions>

## Output Format
<Expected output structure>

## Examples
**Example 1:**
Input: <user prompt>
Output: <expected result>
```

### Description Best Practices

Make descriptions "pushy" - include specific contexts for when to trigger:

```yaml
# BAD - too generic
description: "Create knowledge notes"

# GOOD - pushy with contexts
description: "Create structured Obsidian-style knowledge notes. Use this skill whenever user wants to document concepts, create guides, build knowledge base about specific topics, or capture information - even if they don't explicitly say 'create a note'. Also triggers when user mentions researching, learning about, or documenting subjects."
```

### Required Tools Declaration

Always declare required tools in frontmatter:

```yaml
tools: [filesystem, read, write, glob]
```

---

## Knowledge Note Structure

Each knowledge note follows this structure:

| Element | Required | Description |
|--------|----------|-------------|
| Frontmatter | Yes | type, category, tags, status, created |
| Overview | Yes | 1-2 sentence summary |
| Purpose | Yes | Why this exists |
| Content | Yes | Main explanation |
| Usage | Yes | Practical examples |
| Relationships | Yes | [[Wiki-links]] to related notes |
| Notes | Yes | Important considerations |
| References | Yes | Source links |

### Note Types

| Type | Folder | Use Case |
|------|--------|----------|
| concept | concepts/ | Explanatory content, architecture |
| guide | guides/ | How-to documentation, tutorials |
| reference | references/ | Quick references, commands, cheatsheets |

### Frontmatter Template

```yaml
---
type: <concept|guide|reference>
category: <topic-name>
tags: [<topic>, <subtopic>]
status: active
created: YYYY-MM-DD
---
```

---

## Available Knowledge Topics

| Topic | Concepts | Guides | References | Total |
|-------|----------|--------|------------|-------|
| Kubernetes | 2 | 3 | 2 | 7 |
| Terraform | 1 | 1 | 1 | 3 |
| ArgoCD | 1 | 1 | 1 | 3 |

---

## Tips for Agents

### Creating New Knowledge
1. Use `knowledge-manager` skill
2. Request format: "add [topic name]"
3. Creates folder structure automatically
4. Example: `add docker` → creates `knowledge/docker/`

### Writing Notes
- Use wiki-style links: `[[topic-name]]`
- Group notes by type: `concepts/`, `guides/`, `references/`
- Include practical examples in Usage sections
- Update `INDEX.md` after adding new notes
- NEVER leave empty sections in notes
- Update category INDEX.md when adding new notes

### Conventions
- Category folder = topic name (lowercase, hyphen-separated)
- File path: `knowledge/<category>/<type>/<slug>.md`
- Frontmatter fields: `type`, `category`, `tags`, `status`, `created` (date format: YYYY-MM-DD)

---

## Adding New Topics

1. Use the `knowledge-manager` skill
2. Request: "add [topic name]"
3. Skill creates folder structure automatically

Example flows:

```bash
# Add new topic
"add docker"
→ Creates knowledge/docker/ with concepts/, guides/, references/, INDEX.md

# Document subject
"document Terraform"
→ Creates knowledge/terraform/ with relevant notes

# Research topic
"research Kubernetes ingress"
→ Creates knowledge/kubernetes/ with ingress notes

# Find duplicates
"check for duplicates"
→ Scans knowledge base, reports similarity between notes
```

---

## Skill Creation Best Practices

Based on the `skill-creator` framework:

### Trigger Pattern

```yaml
triggers: [
  "add note",
  "document this",
  "create knowledge",
  "research",
  "learn about",
  "capture",
  "build knowledge"
]
```

### Testing Skills

Create `evals/evals.json` with realistic test cases:

```json
{
  "skill_name": "example-skill",
  "description": "What this skill does",
  "evals": [
    {
      "id": 1,
      "prompt": "User task prompt",
      "expected_output": "Description of expected result",
      "files": []
    }
  ]
}
```

### Output Quality Checklist

- [ ] Frontmatter complete (type, category, tags, status, created)
- [ ] All 7 sections present (Overview, Purpose, Content, Usage, Relationships, Notes, References)
- [ ] No empty sections
- [ ] At least one [[link]] in Relationships
- [ ] Practical examples in Usage section
- [ ] INDEX.md updated for category

---

## Related Files

- See `skill-creator` in `~/.config/opencode/skills/skill-creator/` for full skill creation guide
- See `README.md` for project overview
- Skill path: `~/.config/opencode/skills/skill-creator/`

---

## Quick Reference

| Task | Command |
|-----|---------|
| Add knowledge | "add [topic]" |
| Document subject | "document [subject]" |
| Find duplicates | "find duplicates" |
| Clean up | "clean up notes" |

---

*Last updated: 2026-04-27*