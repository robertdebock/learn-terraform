# Store remote state

|expected time|requirements                                     |
|-------------|-------------------------------------------------|
|60 minutes   |A computer with Terraform installed, lab 10 done.|

## What?

You've learned to work with a local state file so far. When you work with multiple people, you need to share the same state. If you do not share the same state, you can step on each-others toes when applying code.

With remote state, you basically do two things:

1. The state is saved centrally.
2. Locking happens centrally.

Learn how to store remote state:

- [AWS](https://learn.hashicorp.com/tutorials/terraform/aws-remote?in=terraform/aws-get-started).
- [Azure](https://learn.hashicorp.com/tutorials/terraform/azure-remote?in=terraform/azure-get-started).
- [GCP](https://learn.hashicorp.com/tutorials/terraform/google-cloud-platform-outputs?in=terraform/gcp-get-started).

To store the remote state in Azure, this can be used: (Change `MY_STATE_NAME` to something like `robertdebock`.

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
      source  = "hashicorp/azurerm"
      version = "= 2.41.0"
    }
  }
}
```

Run `terraform init` once.

# View the results

| [AWS Console](https://aws.amazon.com/console/) | [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups) | [GCP Console](https://console.cloud.google.com/) |

# Questions:

1. What is so critical about the state?
2. Does the state contain sensitive information?
