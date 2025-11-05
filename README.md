# Terraform AWS IAM User

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

---

## 📘 Description

A Terraform module to create and manage **AWS IAM Users** with optional **access keys**, **login profiles**, **group attachments**, and **managed policy attachments**.
Includes **tagging support** and **secure handling of sensitive outputs** for better security and automation in AWS IAM management.

---

## ⚙️ Features

- 👤 Create AWS IAM Users easily
- 🔑 Optionally generate **access keys** and **login profiles**
- 👥 Attach users to existing **IAM groups**
- 📜 Attach **managed policies** directly to users
- 🏷️ Supports custom **tags** via a tags map
- 🔐 Securely handles **sensitive outputs** (passwords, keys)

---

## 🧱 Provider Requirements

| Name | Version | URL |
|------|----------|-----|
| **AWS Provider** | latest | [AWS Provider Docs](https://registry.terraform.io/providers/hashicorp/aws/latest) |

---

## 🧩 Inputs

| Name | Type | Default | Required | Description |
|------|------|----------|-----------|-------------|
| **name** | `string` | n/a | ✅ Yes | The name of the IAM user. |
| **create_login_profile** | `bool` | `false` | ❌ No | Whether to create a login profile (console password) for the IAM user. |
| **create_access_key** | `bool` | `false` | ❌ No | Whether to create an access key for the IAM user. |
| **groups** | `list(string)` | `[]` | ❌ No | List of IAM group names the user should be added to. |
| **managed_policy_arns** | `list(string)` | `[]` | ❌ No | List of IAM managed policy ARNs to attach to the user. |
| **tags** | `map(string)` | `{}` | ❌ No | A map of tags to assign to the IAM user. |

---
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

## 📤 Outputs

| Name | Description |
|------|--------------|
| `user_name` | The name of the created IAM user. |
| `user_arn` | The Amazon Resource Name (ARN) of the IAM user. |
| `user_unique_id` | The unique ID assigned by AWS to the IAM user. |
| `access_key_id` | The AWS access key ID, if access key creation is enabled. |
| `secret_access_key` | The secret access key value (only available at creation time). |
| `login_profile_password` | The generated password for the IAM console login, if login profile creation is enabled. |
| `groups` | A list of IAM groups that the user is associated with. |
| `attached_policies` | A list of IAM managed policy ARNs attached to the user. |
| `tags` | A mapping of all tags assigned to the IAM user. |
| `name` | The name tag assigned to the IAM user (for reference). |
| `arn` | Alias output for `user_arn` (for compatibility with external references). |


---
### ☁️ Tag Normalization Rules (AWS)

| Cloud | Case      | Allowed Characters | Example                            |
|--------|-----------|------------------|------------------------------------|
| **AWS** | TitleCase | Any              | `Name`, `Environment`, `CostCenter` |

---