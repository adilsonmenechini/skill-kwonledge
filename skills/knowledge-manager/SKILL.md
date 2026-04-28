---
name: knowledge-manager
description: Complete knowledge base management - create, organize, and maintain Obsidian-style knowledge notes. Use this skill for the full knowledge lifecycle: create new notes with proper structure and folder organization, detect and merge duplicate notes, optimize cross-linking, and maintain a clean, usable knowledge base. Also triggers when user wants to add research, document a topic, check for duplicates, clean up notes, or maintain knowledge organization.
triggers: ["add note", "document this", "create knowledge", "research", "learn about", "build knowledge", "capture", "find duplicates", "merge notes", "clean up", "check duplicates", "organization", "maintain knowledge", "optimize knowledge"]
tools: [filesystem, read, write, glob, mkdir, grep]
category: knowledge-management
---

# Knowledge Manager

Complete knowledge base management skill that handles the full knowledge lifecycle: creating new notes, organizing by type, detecting duplicates, and maintaining cross-links.

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
| deepagents | https://docs.deepagents.ai/ |
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
```yaml
---
type: <concept|guide|reference>
category: <category>
tags: []
status: active
created: YYYY-MM-DD
---
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

## Notes
Important considerations.

## References
- [Source](url)
```

---

## Step 5: Create/Update INDEX.md

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
description: Kubernetes (k8s) - Container orchestration platform for automating deployment, scaling, and management of containerized applications. Covers concepts, guides, and references.
tags: ['kubernetes', 'containers', 'orchestration', 'devops', 'cloud-native']
---

# Kubernetes

## Overview
...

*Last updated: 2026-04-27*
```

---

## Step 6: Validate

Check:
- [ ] Category folder exists
- [ ] Type subfolders exist (concepts/, guides/, references/, examples/)
- [ ] Note in correct subfolder
- [ ] INDEX.md exists
- [ ] INDEX.md has frontmatter (name, description, tags)
- [ ] Frontmatter complete
- [ ] All sections present
- [ ] At least one [[link]]
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