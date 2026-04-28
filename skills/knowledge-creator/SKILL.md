---
name: knowledge-creator
description: Create structured Obsidian-style knowledge notes with proper frontmatter, folder structure, and cross-linking. Use this skill whenever the user wants to document a new concept, add study notes, create a reference guide, build their knowledge base about a specific topic, or capture research — even if they don't explicitly say "create a note". Also triggers when user mentions researching a topic, creating documentation about X, writing a guide for Y, or organizing information about a subject.
triggers: ["add kubernetes", "document the", "create note about", "capture", "build knowledge", "research", "learn about", "explain", "document this topic", "add note about", "create documentation"]
tools: [filesystem, read, write, glob, mkdir]
category: knowledge-management
---

# Knowledge Creator

Create new knowledge notes using a standardized Obsidian-compatible structure with proper folder organization. This skill ensures all knowledge notes follow consistent structure with category folders, type subfolders (concepts/guides/references), and proper cross-linking.

---

# When to use

Trigger phrases:
- "add [topic]" or "add [kubernetes]"
- "document [subject]"
- "create note about [topic]"
- "capture information about [subject]"
- "build knowledge base on [topic]"
- "create documentation about [X]"
- "write guide for [X]"
- "research [topic]"
- "learn about [subject]"
- Any request to capture or organize knowledge on a specific topic

---

# Instructions

## Step 1: Identify Topic and Type

### A. Determine the CATEGORY
The category is the TOPIC the user wants to research or document.
- User says "add kubernetes" → category: `kubernetes`
- User says "document React hooks" → category: `react-hooks`
- User says "capture kubernetes information" → category: `kubernetes`

**CRITICAL**: The topic/subject from user's request becomes the folder name (category).

### B. Determine CONTENT TYPE
- Explanatory content → `concept` → goes in `concepts/` folder
- How-to/Process content → `guide` → goes in `guides/` folder
- Quick reference/commands → `reference` → goes in `references/` folder

Default type inference:
| User phrase | Inferred type | Folder |
|-------------|---------------|--------|
| "how does X work" | concept | concepts/ |
| "architecture", "overview" | concept | concepts/ |
| "how to do X" | guide | guides/ |
| "setup", "configure", "tutorial" | guide | guides/ |
| "commands", "reference", "cheatsheet" | reference | references/ |

---

## Step 2: Create Folder Structure (CRITICAL - DO THIS FIRST)

Before creating ANY note, MUST create the folder structure:

```bash
knowledge/
└── <category>/
    ├── concepts/       # Explanatory content
    ├── guides/        # How-to content
    ├── references/    # Quick references/cheatsheets
    └── INDEX.md       # Category index
```

Example for kubernetes:
```bash
knowledge/kubernetes/
├── concepts/
├── guides/
├── references/
└── INDEX.md
```

**IMPORTANT**: Create these directories FIRST using mkdir, then create files inside them.

---

## Step 3: Generate File Path

Format: `knowledge/<category>/<type>/<slug>.md`

| Category | Type | Title | Full Path |
|----------|------|-------|-----------|
| kubernetes | concept | Kubernetes Architecture | knowledge/kubernetes/concepts/kubernetes-architecture.md |
| kubernetes | guide | Kubernetes Deployments | knowledge/kubernetes/guides/kubernetes-deployments.md |
| kubernetes | reference | Kubernetes Services | knowledge/kubernetes/references/kubernetes-services.md |

Slug rules:
- Lowercase only
- Replace spaces with hyphens
- Remove special characters (!@#$%&* etc.)
- Keep it short but descriptive
- Include category prefix for disambiguation

---

## Step 4: Create Note Content

### Frontmatter (REQUIRED - ALL FIELDS)
```yaml
---
type: <concept|guide|reference>
category: <category-name>
tags: [<topic>, <subtopic>]
status: active
created: YYYY-MM-DD
---
```

### Body Sections (ALL 7 REQUIRED)

```markdown
# <Title>

## Overview
Brief explanation of what this is (1-2 sentences max).

## Purpose
Why this exists and when to use it.

## Content
Main explanation with details, examples, and code snippets.

## Usage
Practical examples, commands, or step-by-step instructions.

## Relationships
- [[category-note-slug]] - Brief description of relationship
- [[another-note]] - Another related note

## Notes
Important considerations, limitations, or gotchas.

## References
- [Link to source](url)
```

---

## Step 5: Create Category INDEX.md

File: `knowledge/<category>/INDEX.md`

```markdown
# <Category>

## Overview
Brief description of this knowledge category.

## Notes

### Concepts
- [[concept-slug]] - Brief description

### Guides
- [[guide-slug]] - Brief description

### References
- [[reference-slug]] - Brief description

---

*Last updated: YYYY-MM-DD*
```

---

## Step 6: Add Cross-Linking

FOR EACH note created:
- Add [[link]] to at least one related note in same category
- Update Relationships section with all related notes
- Links should point to notes within same category first

---

## Step 7: Validate Structure

Check EACH item BEFORE finishing:

### Folder Structure
- [ ] Category folder exists: `knowledge/<category>/`
- [ ] Type subfolders exist: `concepts/`, `guides/`, `references/`
- [ ] Note file in CORRECT subfolder (matches type)
- [ ] INDEX.md exists in category folder

### Content
- [ ] Frontmatter has: type, category, tags, status, created
- [ ] All 7 sections present in body
- [ ] No empty sections
- [ ] At least one [[link]] in Relationships section

---

# Rules

1. **ALWAYS create folder structure FIRST** — before creating any note, create directories
2. **Use topic name as category** — extract from user's request
3. **Separate by type** — use concepts/guides/references folders correctly
4. **Never leave placeholders** — fill all sections completely
5. **Cross-link notes** — every note should link to related content
6. **Update INDEX after creation** — keep category index current

---

# Output Expectations

## Correct Folder Structure (REQUIRED)
```
knowledge/
└── <category>/
    ├── concepts/
    │   └── <category>-<topic>.md
    ├── guides/
    │   └── <category>-<topic>.md
    ├── references/
    │   └── <category>-<topic>.md
    └── INDEX.md
```

## WRONG (Do NOT use)
```
knowledge/
├── kubernetes-architecture.md        ❌ WRONG - flat structure
├── kubernetes-deployments.md         ❌ WRONG - flat structure
└── kubernetes-services.md           ❌ WRONG - flat structure
```

## File Requirements
- Self-contained: understandable without reading other notes
- Complete: no empty sections
- Structured: proper frontmatter with all required fields
- Linked: at least one relationship to other notes

---

# Examples

## Example 1: User says "add kubernetes"

1. Category: `kubernetes`
2. Create folder structure FIRST:
   - knowledge/kubernetes/concepts/
   - knowledge/kubernetes/guides/
   - knowledge/kubernetes/references/
3. Create notes in correct folders:
   - `kubernetes/concepts/kubernetes-architecture.md` (concept)
   - `kubernetes/guides/kubernetes-deployments.md` (guide)
   - `kubernetes/references/kubernetes-services.md` (reference)
4. Create `kubernetes/INDEX.md`
5. Add cross-links between notes

## Example 2: User says "how to deploy with Kubernetes"

1. Category: `kubernetes`
2. Type: `guide` (how-to)
3. Path: `knowledge/kubernetes/guides/kubernetes-deployment-guide.md`

---

# References

- resources/template.md
- resources/quality_rules.md
- resources/index_rules.md