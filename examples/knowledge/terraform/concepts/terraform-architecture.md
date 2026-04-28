---
title: Terraform Architecture
type: concept
category: terraform
tags:
  - iac
  - infrastructure-as-code
  - provisioning
  - hashicorp
aliases:
  - terraform-iac
  - tf-architecture
status: active
created: 2026-04-27
updated: 2026-04-27
---

# Terraform Architecture

## Overview
Terraform is an Infrastructure as Code (IaC) tool by HashCorp that defines cloud and on-prem resources in declarative configuration files. It uses a state file to track managed resources.

## Purpose
Terraform enables:
- Version-controlled infrastructure
- Reproducible environments
- Multi-cloud provisioning (AWS, Azure, GCP, etc.)
- Collaboration via shared state
- Drift detection

## Content

### Core Concepts

#### Providers
Plugins that interact with cloud APIs:
```hcl
provider "aws" {
  region = "us-east-1"
}
```

#### Resources
Infrastructure objects to manage:
```hcl
resource "aws_instance" "web" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
}
```

#### Data Sources
Read-only information from providers:
```hcl
data "aws_ami" "ubuntu" {
  most_recent = true
  owners     = ["099720109477"]
}
```

#### Variables
Parameterize configurations:
```hcl
variable "instance_type" {
  type        = string
  default    = "t2.micro"
  description = "EC2 instance type"
}
```

#### Outputs
Expose resource information:
```hcl
output "instance_ip" {
  value = aws_instance.web.public_ip
}
```

### State Management

| State Type | Description |
|------------|-------------|
| Local | File on disk (default) |
| Remote | Shared (S3, etc.) |
| Locking | Prevents concurrent changes |

### Workflow

```
1. Write configuration (.tf)
2. terraform init     # Initialize providers
3. terraform plan   # Preview changes
4. terraform apply # Execute changes
5. terraform destroy # Clean up
```

## Usage

```bash
# Initialize
terraform init

# Plan changes
terraform plan -out=tfplan

# Apply plan
terraform apply tfplan

# Destroy resources
terraform destroy

# Format code
terraform fmt

# Validate
terraform validate
```

## Relationships
- [[terraform-basics]]
- [[terraform-commands]]

## Notes
- State file contains sensitive data - use remote state with encryption
- Providers must be initialized with `terraform init`
- Use workspaces for multi-environment management

## References
- [Terraform Documentation](https://www.terraform.io/docs/)
- [Terraform Registry](https://registry.terraform.io/)