# Skill Kwonledge

Knowledge base repository with Obsidian-style skills and documentation, including best practices from official documentation.

## Project Structure

```
skill-kwonledge/
├── skills/
│   ├── knowledge-manager/   # Create full category structures
│   │   ├── SKILL.md
│   │   ├── evals/
│   │   ├── scripts/          # deduplicate.py, update_schema.py
│   │   └── resources/       # Templates
│   └── knowledge-create/     # Create validated individual notes
│       ├── SKILL.md
│       ├── evals/
│       ├── templates/       # concept, pattern, runbook, architecture
│       ├── validators/       # JSON Schema
│       └── hooks/           # Post-creation actions
├── examples/
│   └── knowledge/
│       ├── kubernetes/      # Container orchestration
│       ├── terraform/       # Infrastructure as Code
│       ├── argocd/          # GitOps continuous delivery
│       ├── deepagents/      # Autonomous AI agents
│       ├── langchain-ai/     # LLM framework
│       └── patterns/        # Reusable patterns (Terragrunt, etc.)
├── AGENTS.md
├── .gitignore
└── README.md
```

## Skills Overview

| Skill | Use Case | Output |
|-------|----------|--------|
| **knowledge-manager** | "add kubernetes" | Full folder structure |
| **knowledge-create** | "create pattern for X" | Single validated note |

### When to Use Each

**knowledge-manager** - Create complete category structure:
- "add [topic]" → creates `knowledge/<topic>/`
- "find duplicates" → deduplication check
- "clean up" → optimize cross-links

**knowledge-create** - Create validated individual notes:
- "create runbook for incident response"
- "document pattern for blue-green deployment"
- "capture architecture for e-commerce"

## Quick Start

### Add New Knowledge (Full Category)

```bash
# Use knowledge-manager skill
"add docker" → creates knowledge/docker/ with structure
```

### Create Individual Note (Validated)

```bash
# Use knowledge-create skill
"create pattern for DRY configs in Terragrunt"
→ Creates knowledge/patterns/terragrunt-dry-configs.md
```

## Knowledge Note Structure

### Folder Organization

```
knowledge/<topic>/
├── concepts/       # Explanatory content
├── guides/         # How-to content
├── references/     # Quick references/commands
├── examples/       # Code examples from official docs
├── patterns/       # Reusable patterns
├── runbooks/       # Operational procedures
└── INDEX.md        # Category index
```

### Note Types (knowledge-create)

| Type | Template | Purpose |
|------|----------|---------|
| concept | concept.md | Definitions, ideas |
| pattern | pattern.md | Solved problems |
| runbook | runbook.md | Procedures |
| architecture | architecture.md | System designs |

## Schema

All notes follow a formal schema:

```yaml
---
id: kubernetes.pods
title: Kubernetes Pods
type: concept
category: kubernetes
domain: kubernetes
tags:
  - containers
  - pods
summary: Brief 1-2 sentence summary
related:
  - [[kubernetes.architecture]]
  - [[kubernetes.services]]
source: https://kubernetes.io/docs/
status: active
version: "1.0.0"
created: 2026-04-27
updated: 2026-04-28
confidence: high
quality_score: 85
---
```

## Available Knowledge

| Topic | Notes | Best Practices |
|-------|-------|----------------|
| Kubernetes | 8 | ✅ Config good practices |
| Terraform | 5 | ✅ Collaborative IaC + Terragrunt |
| ArgoCD | 4 | ✅ GitOps practices |
| Deep Agents | 4 | - |
| LangChain | 4 | - |
| Patterns | 1 | ✅ Terragrunt DRY configs |

### Topics Details

**Kubernetes** - Container orchestration
- architecture, pods, deployments, services, ingress, helm, configmaps-secrets
- Best practices: Health checks, labels, networking, resource limits

**Terraform** - Infrastructure as Code
- architecture, basics, commands, terragrunt-overview
- Best practices: Collaborative IaC, workspace model, Terragrunt patterns

**ArgoCD** - GitOps continuous delivery
- architecture, basics, commands
- Best practices: Separate config repo, immutable manifests

**Deep Agents** - Autonomous AI agents
- architecture, basics, commands

**LangChain** - LLM framework
- fundamentals, getting-started, components

**Patterns** - Reusable Patterns
- terragrunt-dry-configs

## Best Practices Sources

- [Kubernetes Configuration Good Practices](https://kubernetes.io/blog/2025/11/25/configuration-good-practices/)
- [Terraform Recommended Practices](https://developer.hashicorp.com/terraform/cloud-docs/recommended-practices)
- [ArgoCD Best Practices](https://argo-cd.readthedocs.io/en/stable/user-guide/best_practices/)
- [Terragrunt Documentation](https://docs.terragrunt.com/)

## Scripts

### Deduplication Check

```bash
python3 skills/knowledge-manager/scripts/deduplicate.py examples/knowledge/
```

### Schema Update

```bash
python3 skills/knowledge-manager/scripts/update_schema.py
```

## Contributing

1. Use `knowledge-manager` for full categories
2. Use `knowledge-create` for validated individual notes
3. Follow schema and templates
4. Reference official documentation

## Related

- See `AGENTS.md` for detailed agent instructions
- Skill framework: `~/.config/opencode/skills/skill-creator/`
