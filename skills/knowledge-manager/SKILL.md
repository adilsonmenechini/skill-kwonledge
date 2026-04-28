---
name: knowledge-manager
description: Complete knowledge base management - create, organize, and maintain Obsidian-style knowledge notes. Use this skill for the full knowledge lifecycle: create new notes with proper structure and folder organization, detect and merge duplicate notes, optimize cross-linking, and maintain a clean, usable knowledge base. Also triggers when user wants to add research, document a topic, check for duplicates, clean up notes, or maintain knowledge organization.
triggers: ["add note", "document this", "create knowledge", "research", "learn about", "build knowledge", "capture", "find duplicates", "merge notes", "clean up", "check duplicates", "organization", "maintain knowledge", "optimize knowledge"]
tools: [filesystem, read, write, glob, mkdir, grep]
category: knowledge-management
---

# Knowledge Manager

Complete knowledge base management skill that handles the full knowledge lifecycle: creating new notes, organizing by type, detecting duplicates, and maintaining cross-links. Built on Obsidian best practices.

---

# When to use

## Creation Mode Trigger Phrases
- "add [topic]" or "add note about [topic]"
- "document [subject]"
- "create knowledge about [topic]"
- "research [topic]"
- "capture information about [subject]"
- "build knowledge base on [topic]"
- "learn about [subject]"
- "create documentation about [X]"

## Refactor Mode Trigger Phrases
- "find duplicates"
- "check for duplicates"
- "merge notes"
- "clean up notes"
- "deduplicate"
- "fix overlapping notes"
- "organize knowledge"
- "maintain knowledge"

---

# Mode Selection

The skill automatically detects which mode to use:

| User Request | Mode |
|-------------|------|
| New topic to document | Create Mode |
| Add existing knowledge | Create Mode |
| Research something | Create Mode |
| Find duplicates | Refactor Mode |
| Merge notes | Refactor Mode |
| Clean up | Refactor Mode |

---

# CREATE MODE Instructions

Follow these steps when creating new knowledge notes.

## Step 1: Identify Topic and Type

### A. Determine the CATEGORY
Extract topic from user's request:
- "add kubernetes" → category: `kubernetes`
- "document React hooks" → category: `react-hooks`

### B. Determine CONTENT TYPE
- Explanatory content → `concept` → `concepts/` folder
- How-to/Process content → `guide` → `guides/` folder
- Quick reference → `reference` → `references/` folder
- Code examples → `example` → `examples/` folder

Type inference:
| Phrase | Type | Folder |
|--------|------|--------|
| "how does X work" | concept | concepts/ |
| "architecture" | concept | concepts/ |
| "how to do X" | guide | guides/ |
| "setup", "tutorial" | guide | guides/ |
| "commands", "reference" | reference | references/ |
| "example", "code", "sample" | example | examples/ |

---

## Step 2: Create Folder Structure (CRITICAL)

Create before files:

```
knowledge/
└── <category>/
    ├── concepts/
    ├── guides/
    ├── references/
    ├── examples/
    └── INDEX.md
```

**PARA-Inspired Organization** (optional expansion):
- `1. Inbox/` - New notes pending organization
- `2. Projects/` - Active knowledge projects
- `3. Areas/` - Ongoing topics
- `4. Resources/` - Reference materials
- `5. Archive/` - Inactive notes

---

## Step 3: Generate Example from Documentation (CRITICAL)

**IMPORTANT**: When creating a new topic, ALWAYS fetch documentation to create an example in `examples/` folder.

### A. Find Documentation URL

Search for official documentation based on category:

| Category | Documentation |
|----------|---------------|
| kubernetes | https://kubernetes.io/docs/ |
| terraform | https://www.terraform.io/docs/ |
| argocd | https://argo-cd.readthedocs.io/ |
| deepagents | https://docs.langchain.com/oss/python/deepagents/overview |
| langchain-ai | https://python.langchain.com/ |
| docker | https://docs.docker.com/ |
| aws | https://docs.aws.amazon.com/ |

### B. Fetch and Create Example

1. Use web search or fetch to get official documentation
2. Extract a practical code example
3. Create file in `examples/` folder

Example format:
```markdown
---
type: example
category: <category>
tags: [example, code, sample]
status: active
created: YYYY-MM-DD
---

# <Category> Example

## Overview
Practical example demonstrating <topic>.

## Code

```yaml
# or python, bash, etc.
<actual code from documentation>
```

## Explanation

- What this code does
- Key parameters
- How to run it

## Related
- [[<category>-basics]]
- [[<category>-architecture]]
```

---

## Step 4: Generate File Path

Format: `knowledge/<category>/<type>/<slug>.md`

Example:
- kubernetes + concept + architecture → `knowledge/kubernetes/concepts/kubernetes-architecture.md`

Slug rules:
- Lowercase
- Hyphen-separated
- Remove special characters

---

## Step 5: Create Note Content

### Frontmatter (REQUIRED)

Follow Obsidian frontmatter best practices:

```yaml
---
title: <Title>
type: <concept|guide|reference|example>
category: <category>
tags:
  - <tag1>
  - <tag2>
aliases:
  - <alternative-name>
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

**Critical YAML rules:**
- Opening `---` must be on line 1 with no preceding blank lines
- Use **two-space indentation** for list items (not tabs)
- List items must use `- ` (dash + space) prefix
- **NEVER use inline list format**: `[tag1, tag2]` is invalid
- String values with colons should be quoted: `title: "My Note: A Subtitle"`
- Boolean values: `true` / `false` (lowercase, no quotes)
- Dates: ISO 8601 format `YYYY-MM-DD`
- Wikilinks in frontmatter must be quoted: `project: "[[Project Name]]"`
```

### Standard Property Schema

**Core properties (recommended for all notes):**

| Property | Type | Description |
|---------|------|-------------|
| `title` | Text | Human-readable title (often matches filename) |
| `type` | Text | Note type: concept, guide, reference, example |
| `category` | Text | Knowledge category |
| `date` / `created` | Date | Creation date (YYYY-MM-DD) |
| `tags` | List | Topics and categories for filtering |
| `aliases` | List | Alternative names for link suggestions |
| `status` | Text | Current state (e.g., `draft`, `active`, `done`) |
| `updated` | Date | Last update date |

### Extended properties (optional):

```yaml
# For project-like notes
priority: high
due_date: YYYY-MM-DD
stakeholders:
  - "[[Person Name]]"

# For reference notes
source: "https://example.com/article"
author: Author Name

# For learning notes
read_date: YYYY-MM-DD
rating: 1-5
```

### Body Sections (ALL REQUIRED)

```markdown
# <Title>

## Overview
Brief explanation (1-2 sentences).

## Purpose
Why this exists and when to use.

## Content
Main explanation with details.

## Usage
Practical examples and commands.

## Relationships
- [[related-note]]
- [[another-note]]

## Notes
Important considerations.

## References
- [Source](url)
```

---

## Step 6: Use Obsidian Markdown Features

### Wikilinks (Internal Links)

```markdown
[[Note Name]]                          Link to note by name
[[Note Name|Display Text]]             Custom display text
[[Note Name#Heading]]                  Link to a specific heading
[[Note Name#^block-id]]                Link to a specific block
```

### Callouts

Use callouts for highlighted information:

```markdown
> [!note]
> This is a standard note callout.

> [!warning] Custom Title
> Callout with a custom title.

> [!tip]+ Expanded by default
> The + makes this callout expanded.

> [!example]
> Example callout.
```

Common callout types: `note`, `tip`, `warning`, `info`, `example`, `quote`, `bug`, `danger`, `success`, `failure`, `question`, `abstract`, `todo`.

### Block IDs

Add unique IDs for precise linking:

```markdown
This paragraph can be linked from anywhere.
^my-block-id
```

### Tags

Inline tags in body:

```markdown
#tag              # Simple tag
#nested/tag       # Nested tag hierarchy
#category/active # Deep nesting
```

### Embeds

Embed content from other notes:

```markdown
![[Other Note]]              # Embed full note
![[Other Note#Heading]]      # Embed section
![[image.png]]               # Embed image
```

---

## Step 7: Create/Update INDEX.md

**IMPORTANT**: INDEX.md must have YAML frontmatter with name, description, and tags!

In `knowledge/<category>/INDEX.md`:

```markdown
---
name: <category>
description: <description of this knowledge category>
tags: [<tag1>, <tag2>, <tag3>]
---

# <Category>

## Overview
Brief description of this knowledge category.

### Concepts
- [[slug]] - description

### Guides
- [[slug]] - description

### References
- [[slug]] - description

### Examples
- [[<category>-example]] - Practical example from official documentation

---

*Last updated: YYYY-MM-DD*
```

**Example for Kubernetes:**
```markdown
---
name: kubernetes
description: Kubernetes (k8s) - Container orchestration platform...
tags: ['kubernetes', 'containers', 'orchestration', 'devops', 'cloud-native']
---

# Kubernetes

## Overview
...

*Last updated: 2026-04-27*
```

---

## Step 8: Validate

Check:
- [ ] Category folder exists
- [ ] Type subfolders exist (concepts/, guides/, references/, examples/)
- [ ] Note in correct subfolder
- [ ] INDEX.md exists
- [ ] INDEX.md has frontmatter (name, description, tags)
- [ ] Frontmatter uses two-space indentation
- [ ] Frontmatter uses list format for tags (not inline)
- [ ] Dates in ISO 8601 format (YYYY-MM-DD)
- [ ] Frontmatter complete
- [ ] All sections present
- [ ] At least one [[wikilink]]
- [ ] Example file created in examples/ (fetched from official documentation)

---

# REFACTOR MODE Instructions

Follow these steps when refactoring existing knowledge.

## Step 1: Scan Knowledge Base

Traverse all markdown files:

```bash
knowledge/**/*.md
```

Ignore:
- INDEX.md
- Empty files

For each note, extract:
- Title
- Frontmatter
- Content
- Links

---

## Step 2: Normalize Content

For comparison:
- Normalize titles (lowercase, remove special chars)
- Ignore formatting
- Focus on semantic meaning

---

## Step 3: Detect Similarity

### HIGH Similarity (likely duplicate)
- Same or similar title
- Same concept
- Redundant explanations

### MEDIUM Similarity (related)
- Similar sections
- Overlapping examples
- Same domain

### LOW Similarity (ignore)
- Only shared tags
- Weak overlap

---

## Step 4: Generate Report

Output:

```markdown
### HIGH similarity
- [[note-a]] ↔ [[note-b]]
  - reason:

### MEDIUM similarity
- [[note-c]] ↔ [[note-d]]
```

---

## Step 5: Suggest Actions

### HIGH Similarity
- Select primary note (better structure)
- Suggest merge:
  - What to keep
  - What to merge
  - What to remove

### MEDIUM Similarity
- Add [[links]]
- Add cross-references

---

## Step 6: Apply Refactor (ONLY if requested)

### Merge Strategy
1. Keep best structured note
2. Merge unique sections
3. Remove duplicated content
4. Preserve all useful information

### Deprecation Format
```markdown
---
status: deprecated
---

This note has been merged into [[primary-note]].

*Redirected on: YYYY-MM-DD*
```

---

# Rules

1. **Create folder structure FIRST** (create mode)
2. **Use topic as category** - from user's request
3. **Separate by type** - concepts/guides/references/examples
4. **Never placeholders** - fill all sections
5. **Cross-link** - every note links to related content
6. **NEVER auto-delete** - always suggest (refactor mode)
7. **Update INDEX** - after changes
8. **Create examples/ folder** - always include examples/ folder in structure
9. **Frontmatter best practices**:
   - Two-space indentation (no tabs)
   - List format for tags (not inline)
   - ISO 8601 dates (YYYY-MM-DD)
   - Quoted wikilinks in frontmatter
10. **Use Obsidian features** - wikilinks, callouts, block IDs, embeds

---

# Output Expectations

## Create Mode Structure
```
knowledge/
└── <category>/
    ├── concepts/
    │   └── <category>-<topic>.md
    ├── guides/
    ├── references/
    ├── examples/
    │   └── <category>-example.md
    └── INDEX.md
```

## Refactor Mode Output
- Duplicate report grouped by similarity
- Suggested actions for each pair
- Merge suggestions for HIGH similarity

---

# Resources

- resources/template.md
- resources/quality_rules.md
- resources/index_rules.md
