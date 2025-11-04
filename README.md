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

## 🚀 Example Usage

### Basic Usage
```hcl
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
### ☁️ Tag Normalization Rules (AWS)

| Cloud | Case      | Allowed Characters | Example                            |
|--------|-----------|------------------|------------------------------------|
| **AWS** | TitleCase | Any              | `Name`, `Environment`, `CostCenter` |

---
<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.13.4 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 5.1.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 5.1.0 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_labels"></a> [labels](#module\_labels) | opsstation/labels/multicloud | 1.0.0 |

## Resources

| Name | Type |
|------|------|
| [aws_iam_access_key.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_access_key) | resource |
| [aws_iam_user.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user) | resource |
| [aws_iam_user_group_membership.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user_group_membership) | resource |
| [aws_iam_user_login_profile.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user_login_profile) | resource |
| [aws_iam_user_policy.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user_policy) | resource |
| [aws_iam_user_policy_attachment.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user_policy_attachment) | resource |
| [aws_iam_user_ssh_key.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user_ssh_key) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_attributes"></a> [attributes](#input\_attributes) | Additional attributes (e.g. `1`). | `list(any)` | `[]` | no |
| <a name="input_create_iam_user_login_profile"></a> [create\_iam\_user\_login\_profile](#input\_create\_iam\_user\_login\_profile) | Whether to create IAM user login profile | `bool` | `true` | no |
| <a name="input_create_user"></a> [create\_user](#input\_create\_user) | Whether to create the IAM user | `bool` | `true` | no |
| <a name="input_enabled"></a> [enabled](#input\_enabled) | Whether to create Iam user. | `bool` | `true` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | Environment (e.g. `prod`, `dev`, `staging`). | `string` | `""` | no |
| <a name="input_force_destroy"></a> [force\_destroy](#input\_force\_destroy) | When destroying this user, destroy even if it has non-Terraform-managed IAM access keys, login profile or MFA devices. Without force\_destroy a user with non-Terraform-managed access keys and login profile will fail to be destroyed. | `bool` | `false` | no |
| <a name="input_groups"></a> [groups](#input\_groups) | (Optional) List of IAM groups to add the User to. | `list(string)` | `[]` | no |
| <a name="input_label_order"></a> [label\_order](#input\_label\_order) | Label order, e.g. `name`,`application`. | `list(any)` | `[]` | no |
| <a name="input_managedby"></a> [managedby](#input\_managedby) | ManagedBy, eg 'opsstation' | `string` | `"hello@opsstation.com"` | no |
| <a name="input_name"></a> [name](#input\_name) | Name  (e.g. `app` or `cluster`). | `string` | `""` | no |
| <a name="input_password_length"></a> [password\_length](#input\_password\_length) | The length of the generated password | `number` | `20` | no |
| <a name="input_password_reset_required"></a> [password\_reset\_required](#input\_password\_reset\_required) | Whether the user should be forced to reset the generated password on first login. | `bool` | `true` | no |
| <a name="input_path"></a> [path](#input\_path) | The path to the role. | `string` | `"/"` | no |
| <a name="input_permissions_boundary"></a> [permissions\_boundary](#input\_permissions\_boundary) | The ARN of the policy that is used to set the permissions boundary for the role. | `string` | `""` | no |
| <a name="input_pgp_key"></a> [pgp\_key](#input\_pgp\_key) | Either a base-64 encoded PGP public key, or a keybase username in the form keybase:some\_person\_that\_exists. | `string` | `""` | no |
| <a name="input_policy"></a> [policy](#input\_policy) | The policy document. | `any` | `null` | no |
| <a name="input_policy_arn"></a> [policy\_arn](#input\_policy\_arn) | The ARN of the policy you want to apply. | `string` | `""` | no |
| <a name="input_policy_enabled"></a> [policy\_enabled](#input\_policy\_enabled) | Whether to Attach Iam policy with user. | `bool` | `false` | no |
| <a name="input_repository"></a> [repository](#input\_repository) | Terraform current module repo | `string` | `"https://github.com/opsstation/terraform-aws-iam-user"` | no |
| <a name="input_ssh_key_encoding"></a> [ssh\_key\_encoding](#input\_ssh\_key\_encoding) | Specifies the public key encoding format to use in the response. To retrieve the public key in ssh-rsa format, use SSH. To retrieve the public key in PEM format, use PEM | `string` | `"SSH"` | no |
| <a name="input_ssh_public_key"></a> [ssh\_public\_key](#input\_ssh\_public\_key) | The SSH public key. The public key must be encoded in ssh-rsa format or PEM format | `string` | `""` | no |
| <a name="input_status"></a> [status](#input\_status) | The access key status to apply. Defaults to Active. Valid values are Active and Inactive. | `string` | `"Active"` | no |
| <a name="input_upload_iam_user_ssh_key"></a> [upload\_iam\_user\_ssh\_key](#input\_upload\_iam\_user\_ssh\_key) | Whether to upload a public ssh key to the IAM user | `bool` | `false` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_arn"></a> [arn](#output\_arn) | The ARN assigned by AWS for this user. |
| <a name="output_key_id"></a> [key\_id](#output\_key\_id) | The access key ID. |
| <a name="output_secret"></a> [secret](#output\_secret) | The secret access key. Note that this will be written to the state file. Please supply a pgp\_key instead, which will prevent the secret from being stored in plain text. |
| <a name="output_tags"></a> [tags](#output\_tags) | A mapping of tags to assign to the resource. |
| <a name="output_unique_id"></a> [unique\_id](#output\_unique\_id) | The unique ID assigned by AWS for this user. |
<!-- END_TF_DOCS -->