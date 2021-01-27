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

A few extra steps are required for Azure, as [documented](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/guides/service_principal_client_secret#configuring-the-service-principal-in-terraform):

On your terminal:

1. Get the `id` using `az account list`.
2. Get the `appId, `password` and `tenant` using `az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${id}"

Now go to [Terraform Cloud](https://app.terraform.io/) -> Workspaces -> ${workspace} -> Variables - Environment Variables.

1. Add `ARM_CLIENT_ID` with the value from `appId`.
2. Add `ARM_CLIENT_SECRET` with the value from `password`.
3. Add `ARM_TENANT_ID` with the value from `tenant`.
4. Add `ARM_SUBSCRIPTION_ID` with the value from `id` from the first command.

While having [Terraform Cloud](https://app.terraform.io/) opend, you can run:

- `terraform init`
- `terraform plan`
- `terraform apply`

# View the results

| [AWS Console](https://aws.amazon.com/console/) | [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups) | [GCP Console](https://console.cloud.google.com/) |

# Questions:

1. What is so critical about the state?
2. Does the state contain sensitive information?
