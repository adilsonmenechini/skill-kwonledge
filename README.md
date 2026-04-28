# Skill Kwonledge

Knowledge base repository with Obsidian-style skills and documentation.

## Project Structure

```
skill-kwonledge/
├── skills/              # OpenCode skills
│   ├── knowledge-manager/   # Unified skill (create + refactor)
│   ├── knowledge-creator/  # Create notes only
│   └── knowledge-refactor/ # Refactor only
├── examples/          # Knowledge base
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

## Available Knowledge

| Topic | Concepts | Guides | References | Examples |
|-------|----------|--------|------------|----------|
| Kubernetes | 2 | 3 | 2 | 1 |
| Terraform | 1 | 1 | 1 | 1 |
| ArgoCD | 1 | 1 | 1 | 1 |
| Deep Agents | 1 | 1 | 1 | 1 |
| LangChain | 1 | 1 | 1 | 1 |

### Topics Details

**Kubernetes** - Container orchestration
- architecture, pods, deployments, services, ingress, helm, configmaps-secrets

**Terraform** - Infrastructure as Code
- architecture, basics, commands

**ArgoCD** - GitOps continuous delivery
- architecture, basics, commands

**Deep Agents** - Autonomous AI agents
- architecture, basics, commands

**LangChain** - LLM framework
- fundamentals, getting-started, components

## Contributing

1. Use `knowledge-manager` skill
2. Ask: "add [topic]"
3. Creates folder structure automatically with examples from official docs

## Related

- See `AGENTS.md` for detailed agent instructions
- Skill framework: `~/.config/opencode/skills/skill-creator/`
