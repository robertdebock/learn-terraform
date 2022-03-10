# Store remote state

|expected time|requirements                                     |
|-------------|-------------------------------------------------|
| 60 minutes  | A computer with Terraform installed.            |

Goal: Learn how to store remote state:

## Explanation

You've learned to work with a local state file so far. When you work with multiple people, you need to share the same state. If you do not share the same state, you can step on each-others toes when applying code.

With remote state, you basically do two things:

1. The state is saved centrally.
2. Locking happens centrally.

## Howto

For "generic" use of cloud providers you can follow:

- [AWS](https://learn.hashicorp.com/tutorials/terraform/aws-remote?in=terraform/aws-get-started).
- [Azure](https://learn.hashicorp.com/tutorials/terraform/azure-remote?in=terraform/azure-get-started).
- [GCP](https://learn.hashicorp.com/tutorials/terraform/google-cloud-platform-outputs?in=terraform/gcp-get-started).

For our environment, we'll store the state and lock in a azure container.

To store the remote state in Azure, this can be used: (Change `MY_STATE_NAME` to something like `robertdebock`.

Change the `terraform` parameter in `main.tf` to this.

```hcl
terraform {
  backend "azurerm" {
  resource_group_name  = "rg-terraform-cmn-sbx"
  storage_account_name = "stterraformcmnsbx"
  container_name       = "c-terraform"
  key                  = "rg-MY_STATE_NAME-sbx.tfstate"
  }
  required_providers {
    azurerm = {
      source = "hashicorp/azurerm"
      version = ">= 2.26"
    }
  }
}
```

## Assignment

- [ ] Add the remote backend to your `main.tf`.
- [ ] Run `terraform init`.
- [ ] Verify the results.

## Questions:

1. What is so critical about the state?
2. Does the state contain sensitive information?
3. What have you solved now that the state is remote?
