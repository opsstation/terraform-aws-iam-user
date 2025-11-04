 # Terraform-aws-iam-user

[![OpsStation](https://img.shields.io/badge/Made%20by-OpsStation-blue?style=flat-square&logo=terraform)](https://www.opsstation.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Terraform](https://img.shields.io/badge/Terraform-1.13%2B-purple.svg?logo=terraform)](#)
[![CI](https://github.com/OpsStation/terraform-multicloud-labels/actions/workflows/ci.yml/badge.svg)](https://github.com/OpsStation/terraform-multicloud-labels/actions/workflows/ci.yml)

> 🌩️  **A production-grade, reusable AWS Subnet module by [OpsStation](https://www.opsstation.com)**
> Designed for reliability, performance, and security — following AWS networking best practices.
---

## 🏢 About OpsStation

**OpsStation** delivers **Cloud & DevOps excellence** for modern teams:
- 🚀 **Infrastructure Automation** with Terraform, Ansible & Kubernetes
- 💰 **Cost Optimization** via scaling & right-sizing
- 🛡️  **Security & Compliance** baked into CI/CD pipelines
- ⚙️ **Fully Managed Operations** across AWS, Azure, and GCP

> 💡 Need enterprise-grade DevOps automation?
> 👉 Visit [**www.opsstation.com**](https://www.opsstation.com) or email **hello@opsstation.com**

---
🌟 Features – Terraform AWS IAM User Module

- Creates and manages AWS IAM Users with optional login profile and access keys
- Supports multiple IAM users creation using count or for_each
- Allows configuration of user policies, inline policies, and managed policy attachments
- Supports creation of PGP-encrypted access keys for secure key delivery
- Provides option to configure user path, permissions boundaries, and tags
- Automatically integrates tagging via the Labels Module for consistent naming
- Supports conditional resource creation using enabled flag
- Compatible with OpsStation Terraform Modules for KMS, IAM Roles, and Policies
- Ensures least-privilege access principle by supporting fine-grained policy attachments
- Outputs detailed information such as user name, ARN, and access key details
- Designed for secure, scalable, and modular IAM user management

# Example
```hcl
module "iam-user" {
  source      = "git::https://github.com/opsstation/terraform-aws-iam-user.git?ref=v1.0.0"

  name        = "iam-user"
  environment = "test"
  label_order = ["name", "environment"]

  policy_enabled          = false
  policy                  = data.aws_iam_policy_document.default.json
  pgp_key                 = ""
  password_length         = 20
  password_reset_required = true
}

data "aws_iam_policy_document" "default" {
  statement {
    actions = [
      "ec2:Describe*"
    ]
    effect    = "Allow"
    resources = ["*"]
  }
}
```
## 📤 Outputs

| **Name**                | **Description**                                                                 |
| ------------------------ | ------------------------------------------------------------------------------- |
| `user_name`              | The name of the created IAM user.                                               |
| `user_arn`               | The Amazon Resource Name (ARN) of the IAM user.                                 |
| `user_unique_id`         | The unique ID assigned by AWS to the IAM user.                                  |
| `access_key_id`          | The AWS access key ID, if access key creation is enabled.                       |
| `secret_access_key`      | The secret access key value (only available at creation time).                  |
| `login_profile_password` | The generated password for the IAM console login, if login profile creation is enabled. |
| `groups`                 | A list of IAM groups that the user is associated with.                          |
| `attached_policies`      | A list of IAM managed policy ARNs attached to the user.                         |
| `tags`                   | A mapping of all tags assigned to the IAM user.                                 |
| `name`                   | The name tag assigned to the IAM user (for reference).                          |
| `arn`                    | Alias output for `user_arn` (for compatibility with external references).       |

---
### ☁️ Tag Normalization Rules (AWS)

| Cloud | Case      | Allowed Characters | Example                            |
|--------|-----------|------------------|------------------------------------|
| **AWS** | TitleCase | Any              | `Name`, `Environment`, `CostCenter` |

---

### 💙 Maintained by [OpsStation](https://www.opsstation.com)
> OpsStation — Simplifying Cloud, Securing Scale.