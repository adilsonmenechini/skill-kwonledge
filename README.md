# Skill Kwonledge

Knowledge base repository with Obsidian-style skills and documentation.

## Project Structure

```
skill-kwonledge/
├── skills/              # OpenCode skills
│   ├── knowledge-manager/   # Unified skill (create + refactor)
│   ├── knowledge-creator/  # Create notes only
│   └── knowledge-refactor/ # Refactor only
├── skills-bkp/         # Backup of original skills
├── examples/          # Knowledge base (kubernetes, terraform, argocd)
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
├── references/    # Quick references/commands
└── INDEX.md      # Category index
```

## Available Knowledge

| Topic | Notes |
|-------|-------|
| Kubernetes | architecture, pods, deployments, services, ingress, helm |
| Terraform | architecture, basics, commands |
| ArgoCD | architecture, basics, commands |

## Contributing

1. Use `knowledge-manager` skill
2. Ask: "add [topic]"
3. Creates folder structure automatically

## Related

- See `AGENTS.md` for detailed agent instructions