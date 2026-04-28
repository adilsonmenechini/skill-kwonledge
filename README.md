# Skill Kwonledge

Knowledge base repository with Obsidian-style skills and documentation, including best practices from official documentation.

## Project Structure

```
skill-kwonledge/
├── skills/
│   └── knowledge-manager/   # Unified skill (create + refactor)
│       ├── SKILL.md           # Main skill
│       ├── evals/            # Test cases
│       ├── scripts/           # Automation scripts
│       └── resources/         # Templates
├── examples/
│   └── knowledge/
│       ├── kubernetes/      # Container orchestration
│       ├── terraform/      # Infrastructure as Code
│       ├── argocd/         # GitOps continuous delivery
│       ├── deepagents/     # Autonomous AI agents
│       └── langchain-ai/  # LLM framework
├── AGENTS.md          # Agent instructions
├── .gitignore
└── README.md
```

## Quick Start

### Add New Knowledge

```bash
# Use the knowledge-manager skill
"add docker"  → creates knowledge/docker/ with structure
```

### Structure Created

```
knowledge/<topic>/
├── concepts/       # Explanatory content
├── guides/        # How-to content  
├── references/   # Quick references/commands
├── examples/     # Code examples from official docs
└── INDEX.md      # Category index
```

## Schema

All notes follow a formal schema with frontmatter:

```yaml
---
id: kubernetes.pods
title: Kubernetes Pods
type: concept
category: kubernetes
tags:
  - containers
  - pods
status: active
version: "1.0.0"
created: 2026-04-27
updated: 2026-04-28
confidence: high
source: docs
inputs: []
outputs: []
dependencies: []
quality_score: 85
---
```

## Available Knowledge

| Topic | Notes | Best Practices |
|-------|-------|--------------|
| Kubernetes | 8 | ✅ Config good practices |
| Terraform | 4 | ✅ Collaborative IaC |
| ArgoCD | 4 | ✅ GitOps practices |
| Deep Agents | 4 | - |
| LangChain | 4 | - |

### Topics Details

**Kubernetes** - Container orchestration
- architecture, pods, deployments, services, ingress, helm, configmaps-secrets
- Best practices: Health checks, labels, networking, resource limits

**Terraform** - Infrastructure as Code
- architecture, basics, commands
- Best practices: Collaborative IaC, workspace model, four personas

**ArgoCD** - GitOps continuous delivery
- architecture, basics, commands
- Best practices: Separate config repo, immutable manifests

**Deep Agents** - Autonomous AI agents
- architecture, basics, commands

**LangChain** - LLM framework
- fundamentals, getting-started, components

## Best Practices Sources

- [Kubernetes Configuration Good Practices](https://kubernetes.io/blog/2025/11/25/configuration-good-practices/)
- [Terraform Recommended Practices](https://developer.hashicorp.com/terraform/cloud-docs/recommended-practices)
- [ArgoCD Best Practices](https://argo-cd.readthedocs.io/en/stable/user-guide/best_practices/)

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

1. Use `knowledge-manager` skill
2. Ask: "add [topic]"
3. Creates folder structure automatically with examples from official docs

## Related

- See `AGENTS.md` for detailed agent instructions
- Skill framework: `~/.config/opencode/skills/skill-creator/`
