---
name: knowledge-refactor
description: Detect duplicate or highly similar knowledge notes and propose safe merges or structural improvements. Use this skill during periodic knowledge base cleanup, before building RAG or embeddings, when the user notices overlapping notes, or when explicitly asked to merge, deduplicate, or clean up notes. NEVER auto-delete — always propose actions first.
triggers: ["find duplicates", "merge notes", "clean up notes", "deduplicate", "check for duplicates", "fix overlapping notes"]
tools: [filesystem, read, glob, grep]
---

# Purpose

Identify duplicate, overlapping, or highly similar knowledge notes and improve overall consistency by suggesting safe refactors such as merging or linking.

---

# When to use

Use this skill when:

- The knowledge base is growing and may contain duplication
- You want to improve consistency and structure
- Before building RAG or embeddings
- During periodic cleanup or refactoring

---

# Instructions

## 1. Scan knowledge base

Traverse all markdown files:

knowledge/**/*.md

Ignore:
- INDEX.md
- Files with no meaningful content

For each note, extract:

- title
- frontmatter (type, category, tags, status)
- sections and content

---

## 2. Normalize content

For comparison:

- Normalize titles (lowercase, remove symbols)
- Ignore formatting differences
- Focus on semantic meaning

---

## 3. Detect similarity

Compare notes using signals:

### Strong signals
- Same or very similar title
- Same concept described
- Redundant explanations

### Medium signals
- Similar sections or structure
- Overlapping examples
- Same problem domain

### Weak signals
- Shared tags
- Same category

---

## 4. Classify similarity

For each pair:

- HIGH → likely duplicate
- MEDIUM → related or partially overlapping
- LOW → ignore

---

## 5. Generate report

Output grouped results:

### HIGH similarity
- note A
- note B
- reason

### MEDIUM similarity
- possible relationship

---

## 6. Suggest actions

### For HIGH similarity

- Select a primary note (best structured)
- Suggest merge:
  - what to keep
  - what to merge
  - what to remove

### For MEDIUM similarity

- Suggest:
  - adding [[links]]
  - cross-references

---

## 7. Optional: apply refactor (ONLY if explicitly requested)

### Merge strategy

1. Keep best structured note
2. Merge missing or unique sections
3. Remove duplicated content
4. Preserve all useful information

### Deprecation format

When merging, replace the secondary note content with:

```markdown
---
status: deprecated
---

This note has been merged into [[primary-note]].

---

*Redirected on: YYYY-MM-DD*
```

**Safe mode**: If uncertain about merge, add cross-links instead.

---

# Rules

- NEVER delete content automatically
- NEVER overwrite without explicit instruction
- ALWAYS preserve information
- Prefer linking over merging when uncertain
- Maintain Obsidian-compatible [[links]]

---

# Output format

## Duplicate Report

### HIGH
- [[note-a]] ↔ [[note-b]]
  - reason:

### MEDIUM
- [[note-c]] ↔ [[note-d]]

---

## Suggested Actions

- Merge [[note-a]] into [[note-b]]
- Link [[note-c]] ↔ [[note-d]]

---

# References

- resources/similarity_rules.md
- resources/merge_strategy.md