---
name: knowledge-manager
description: Complete knowledge base management - create, organize, and maintain Obsidian-style knowledge notes. Use this skill for the full knowledge lifecycle: create new notes with proper structure and folder organization, detect and merge duplicate notes, optimize cross-linking, and maintain a clean, usable knowledge base. Also triggers when user wants to add research, document a topic, check for duplicates, clean up notes, or maintain knowledge organization.
tags: ['skill']
---

# Knowledge Manager - INDEX

## Overview
This skill provides complete knowledge base management combining creation and refactor capabilities in a single unified interface.

## Modes

### CREATE Mode
**Trigger**: "add [topic]", "document X", "create knowledge", "research"

Creates knowledge notes with:
- Folder structure (concepts/, guides/, references/)
- Proper frontmatter (type, category, tags, status, created)
- Complete sections (Overview, Purpose, Content, Usage, Relationships, Notes, References)
- Cross-linking between related notes
- INDEX.md with category overview

### REFACTOR Mode
**Trigger**: "find duplicates", "merge notes", "clean up", "deduplicate"

Manages existing knowledge:
- Scan for duplicate/similar notes
- Similarity classification (HIGH/MEDIUM/LOW)
- Merge suggestions
- Cross-linking optimization

## Content

### Concepts
- [[kubernetes-architecture]] - Kubernetes core architecture
- [[terraform-architecture]] - Terraform architecture
- [[kubernetes-pods]] - Kubernetes Pods

### Guides
- [[kubernetes-deployments]] - Kubernetes Deployments
- [[kubernetes-ingress]] - Kubernetes Ingress
- [[kubernetes-helm]] - Helm package manager
- [[terraform-basics]] - Terraform basics

### References
- [[kubernetes-services]] - Kubernetes Services
- [[kubernetes-configmaps-secrets]] - ConfigMaps and Secrets
- [[terraform-commands]] - Terraform CLI commands

## Notes

### Available Topics
- **Kubernetes**: container orchestration, deployments, services, networking
- **Terraform**: infrastructure as code, provisioning, HCL

### Adding New Topics
Request format: "add [topic]" or "document [subject]"

Example: "add docker" creates:
```
knowledge/docker/
├── concepts/
├── guides/
├── references/
└── INDEX.md
```

## Relationships
- [[knowledge-creator]]
- [[knowledge-refactor]]

---

*Last updated: 2026-04-27*