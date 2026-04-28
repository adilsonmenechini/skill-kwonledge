---
id: terragrunt.concept.overview
title: Terragrunt Overview
type: concept
domain: terragrunt
tags:
  - terragrunt
  - terraform
  - iac
  - infrastructure-as-code
  - open-tofu
summary: Terragrunt is a thin wrapper for OpenTofu/Terraform that provides extra tools for keeping your configurations DRY, managing remote state, and working with multiple Terraform modules.
related:
  - terraform.architecture
  - terraform.basics
source: https://docs.terragrunt.com/getting-started/overview
created_at: 2026-04-28
updated_at: 2026-04-28
confidence: high
version: "1.0.0"
quality_score: 90
---

# Terragrunt Overview

## 🧠 Definition

Terragrunt is a thin wrapper for OpenTofu/Terraform that provides extra tools for keeping your configurations DRY (Don't Repeat Yourself), managing remote state, and working with multiple Terraform modules. It aims to solve the scaling problems that teams encounter when managing infrastructure as code.

## 📚 Explanation

### What Terragrunt Adds

Unlike plain Terraform, Terragrunt provides:

1. **DRY Configurations**: Use `include` blocks to share configuration across units
2. **Remote State Management**: Automatic S3/DynamoDB setup for state storage
3. **Dependency Management**: Built-in dependency resolution with DAG
4. **Code Generation**: Generate provider.tf and backend.tf automatically
5. **Multiple Module Support**: Manage stacks of interdependent modules

### How It Works

Terragrunt reads `terragrunt.hcl` files and:
1. Downloads Terraform modules to `.terragrunt-cache/`
2. Generates configuration files (provider, backend)
3. Orchestrates Terraform commands with proper ordering

```hcl
# Example terragrunt.hcl
remote_state {
  backend = "s3"
  config = {
    bucket = "my-terraform-state"
    key = "env:/dev/terraform.tfstate"
    region = "us-east-1"
  }
}

generate "provider" {
  path = "provider.tf"
  contents = <<EOF
provider "aws" {
  region = "us-east-1"
}
EOF
}

terraform {
  source = "tfr:///terraform-aws-modules/vpc/aws?version=5.16.0"
}

inputs = {
  name = "my-vpc"
  cidr = "10.0.0.0/16"
}
```

## 🔗 Related

- [[terraform.architecture]] - Terraform architecture
- [[terraform.basics]] - Terraform basics

## 🧩 Key Insights

- **Orchestrator Pattern**: Terragrunt operates at a higher abstraction level than Terraform
- **Hermetic Units**: Each unit is an isolated, reproducible container
- **Stack Definition**: A stack is a collection of units that can be reasoned about together
- **DRY Principle**: Configuration hierarchy prevents code duplication

## ⚠️ Trade-offs

- **Additional Abstraction**: Adds learning curve on top of Terraform
- **Cache Storage**: Uses `.terragrunt-cache/` which requires disk space
- **Version Constraints**: Requires compatible Terraform/OpenTofu versions

## 📊 Observability

- **Logging**: Detailed contextual logging with module prefixes
- **Run Reports**: Built-in reporting for stack operations
- **Graph Support**: DAG visualization with `terragrunt dag graph`

## 📚 References

- [Terragrunt Documentation](https://docs.terragrunt.com/)
- [Terragrunt GitHub](https://github.com/gruntwork-io/terragrunt)