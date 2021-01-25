# Destroy infrastructure

|expected time|requirements                                    |
|-------------|------------------------------------------------|
|15 minutes   |A computer with terraform installed, lab 6 done.|

Learn how to destroy infrastructure:

- [AWS](https://learn.hashicorp.com/tutorials/terraform/aws-destroy?in=terraform/aws-get-started).
- [Azure](https://learn.hashicorp.com/tutorials/terraform/azure-destroy?in=terraform/azure-get-started).
- [GCP](https://learn.hashicorp.com/tutorials/terraform/google-cloud-platform-destroy?in=terraform/gcp-get-started).

# View the results

| [AWS Console](https://aws.amazon.com/console/) | [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups) | [GCP Console](https://console.cloud.google.com/) |

# Questions:

1. Now that you know how to destroy all resources defined, how do you destroy only on resource?
2. Why would you use `terraform destroy`?
3. Can you destroy without `terraform.tfstate` or `terraform.tfstate.backup`?
