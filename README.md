# # 🏗️ Terraform AWS IAM User


[![OpsStation](https://img.shields.io/badge/Made%20by-OpsStation-blue?style=flat-square&logo=terraform)](https://www.opsstation.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Terraform](https://img.shields.io/badge/Terraform-1.13%2B-purple.svg?logo=terraform)](#)
[![CI](https://github.com/OpsStation/terraform-aws-ec2/actions/workflows/ci.yml/badge.svg)](https://github.com/OpsStation/terraform-aws-ec2/actions/workflows/ci.yml)

> 🌩️ **A production-grade, reusable AWS Ec2 module by [OpsStation](https://www.opsstation.com)**
> Designed for reliability, performance, and security — following AWS networking best practices.
---

## 🏢 About OpsStation

**OpsStation** delivers **Cloud & DevOps excellence** for modern teams:
- 🚀 **Infrastructure Automation** with Terraform, Ansible & Kubernetes
- 💰 **Cost Optimization** via scaling & right-sizing
- 🛡️ **Security & Compliance** baked into CI/CD pipelines
- ⚙️ **Fully Managed Operations** across AWS, Azure, and GCP

> 💡 Need enterprise-grade DevOps automation?
> 👉 Visit [**www.opsstation.com**](https://www.opsstation.com) or email **hello@opsstation.com**

---

## 🌟 Features

- ✅ Creates and manages **AWS IAM Users** with customizable configurations
- ✅ Supports attaching **managed** and **inline IAM policies** to users
- ✅ Optionally adds users to existing **IAM Groups**
- ✅ Enables generation and management of **access keys** for programmatic access
- ✅ Supports **login profile creation** for AWS Management Console access
- ✅ Configurable **permissions boundaries**, **path**, and **tags**
- ✅ Integrates seamlessly with **AWS IAM Policies**, **Roles**, and **Groups**
- ✅ Enforces AWS best practices for **least-privilege** and **secure identity management**
- ✅ Fully compatible with other **OpsStation Terraform modules**


## 🚀 Example Usage

### Basic Usage

module "iam_user" {
  source = "path/to/terraform-aws-iam-user"

  name                 = "dev-user"
  create_login_profile = true
  create_access_key    = true
  groups               = ["developers"]
  managed_policy_arns  = ["arn:aws:iam::aws:policy/AdministratorAccess"]

  tags = {
    Environment = "dev"
    Project     = "app1"
  }
}

---
### 🔐 Outputs (AWS IAM User Module)

| Name                     | Description                                                                 |
|---------------------------|------------------------------------------------------------------------------|
| `id`                      | The unique identifier (ID) of the created **IAM User**.                     |
| `arn`                     | The ARN (Amazon Resource Name) of the created **IAM User**.                 |
| `name`                    | The name of the created **IAM User**.                                       |
| `path`                    | The path to the IAM User within AWS IAM.                                   |
| `create_date`             | The date and time when the IAM User was created.                            |
| `unique_id`               | The stable and unique string identifying the IAM User.                      |
| `user_policy_arns`        | A list of attached **managed policy ARNs** associated with the IAM User.    |
| `inline_policies`         | A map of **inline IAM policies** directly attached to the IAM User.         |
| `permissions_boundary`    | The ARN of the **permissions boundary policy** attached to the IAM User (if any). |
| `login_profile`           | Details of the **login profile** (if console access is enabled).            |
| `access_key_id`           | The **Access Key ID** created for programmatic access (if configured).      |
| `secret_access_key`       | The **Secret Access Key** created for programmatic access (if configured).  |
| `tags`                    | A mapping of **tags** assigned to the IAM User.                             |

### ☁️ Tag Normalization Rules (AWS)

| Cloud | Case      | Allowed Characters | Example                            |
|--------|-----------|------------------|------------------------------------|
| **AWS** | TitleCase | Any              | `Name`, `Environment`, `CostCenter` |

---

### 💙 Maintained by [OpsStation](https://www.opsstation.com)
> OpsStation — Simplifying Cloud, Securing Scale.
