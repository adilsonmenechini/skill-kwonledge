---
name: knowledge-base
description: Knowledge base with Obsidian-style notes covering various technical topics. Includes Kubernetes, Terraform (with Terragrunt), ArgoCD, Deep Agents, LangChain, and patterns. Each topic has concepts (explanatory), guides (how-to), references (commands), and examples.
tags:
  - knowledge-base
  - documentation
  - obsidian
  - devops
  - ai
  - llm
  - patterns
  - terraform
  - terragrunt
aliases:
  - kb
  - knowledge
---

# Knowledge Base

## Overview
This is the main knowledge base index containing all documented topics.

## Topics

### Kubernetes
- [[kubernetes-architecture]] - Container orchestration architecture
- [[kubernetes-pods]] - Pods concept
- [[kubernetes-deployments]] - Deployments guide
- [[kubernetes-services]] - Services reference
- [[kubernetes-ingress]] - Ingress guide
- [[kubernetes-helm]] - Helm guide
- [[kubernetes-configmaps-secrets]] - ConfigMaps & Secrets
- [[kubernetes-deployment-example]] - Deployment + Service example

### Terraform
- [[terraform-architecture]] - Infrastructure as Code architecture
- [[terraform-basics]] - Getting started with Terraform
- [[terraform-commands]] - CLI commands reference
- [[terraform-ec2-example]] - EC2 instance example

### Terragrunt
- [[terragrunt-overview]] - Terragrunt overview (wrapper for Terraform)
- [[terragrunt-commands]] - Terragrunt CLI commands
- [[terragrunt-vpc-example]] - VPC example

### Ansible
- [[ansible-overview]] - IT automation overview
- [[ansible-directory-layout]] - Directory layout best practices
- [[ansible-commands]] - CLI commands reference

### ArgoCD
- [[argo-workflows-architecture]] - GitOps continuous delivery architecture
- [[argocd-basics]] - Getting started with ArgoCD
- [[argocd-commands]] - CLI commands reference
- [[argocd-application-example]] - Application example

### Deep Agents
- [[deepagents-architecture]] - Autonomous AI agents architecture
- [[deepagents-basics]] - Getting started with Deep Agents
- [[deepagents-commands]] - API reference
- [[deepagents-quickstart]] - Quickstart example

### LangChain
- [[langchain-fundamentals]] - Core components and concepts
- [[langchain-getting-started]] - Getting started tutorial
- [[langchain-components]] - Components reference
- [[langchain-lcel-example]] - LCEL chain example

### Patterns
- [[clawteam]] - Agent Swarm Intelligence pattern
- [[terragrunt-dry-configs]] - Terragrunt DRY configuration pattern

## Adding New Topics

**For full category structure:**
- Use `knowledge-manager` skill: "add [topic]"

**For individual validated notes:**
- Use `knowledge-create` skill: "create pattern for X"

Example:
- "add docker" → creates `knowledge/docker/` structure
- "document AWS" → creates `knowledge/aws/` structure
- "create pattern for caching" → creates `knowledge/patterns/caching.md`

---

*Last updated: 2026-04-28*