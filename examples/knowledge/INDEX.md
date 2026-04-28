---
name: knowledge-base
description: Knowledge base with Obsidian-style notes organized by category (IaC, DevOps, AI). Each category contains topics with concepts, guides, references, and examples.
tags:
  - knowledge-base
  - documentation
  - obsidian
  - iac
  - devops
  - ai
  - patterns
aliases:
  - kb
  - knowledge
---

# Knowledge Base

## Overview
This is the main knowledge base index, organized by category.

## Categories

| Category | Topics |
|----------|-------|
| [[IaC]] | Terraform, Terragrunt, Ansible |
| [[DevOps]] | Kubernetes, ArgoCD |
| [[AI]] | Deep Agents, LangChain |
| [[Patterns]] | Cross-category patterns |

## Topics by Category

### IaC (Infrastructure as Code)
- [[terraform-architecture]] - Terraform IaC
- [[terraform-basics]] - Terraform basics
- [[terraform-commands]] - Terraform CLI
- [[terraform-ec2-example]] - Terraform EC2
- [[terragrunt-overview]] - Terragrunt overview
- [[terragrunt-commands]] - Terragrunt CLI
- [[terragrunt-vpc-example]] - Terragrunt VPC
- [[ansible-overview]] - Ansible overview
- [[ansible-directory-layout]] - Ansible directory layout
- [[ansible-commands]] - Ansible CLI

### DevOps
- [[kubernetes-architecture]] - Kubernetes architecture
- [[kubernetes-pods]] - Pods
- [[kubernetes-deployments]] - Deployments
- [[kubernetes-services]] - Services
- [[kubernetes-ingress]] - Ingress
- [[kubernetes-helm]] - Helm
- [[kubernetes-configmaps-secrets]] - ConfigMaps & Secrets
- [[kubernetes-deployment-example]] - K8s deployment example
- [[argo-workflows-architecture]] - ArgoCD architecture
- [[argocd-basics]] - ArgoCD basics
- [[argocd-commands]] - ArgoCD CLI
- [[argocd-application-example]] - ArgoCD app example

### AI
- [[deepagents-architecture]] - Deep Agents architecture
- [[deepagents-basics]] - Deep Agents basics
- [[deepagents-commands]] - Deep Agents API
- [[deepagents-quickstart]] - Deep Agents quickstart
- [[langchain-fundamentals]] - LangChain fundamentals
- [[langchain-getting-started]] - LangChain getting started
- [[langchain-components]] - LangChain components
- [[langchain-lcel-example]] - LangChain LCEL

### Patterns
- [[clawteam]] - Agent Swarm Intelligence pattern
- [[terragrunt-dry-configs]] - Terragrunt DRY pattern

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