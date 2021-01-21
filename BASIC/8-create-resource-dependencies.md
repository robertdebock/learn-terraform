# Create resource dependencies

|expected time|requirements                                    |
|-------------|------------------------------------------------|
|30 minutes   |A computer with terraform installed, lab 7 done.|

Learn how dependecies work in Terraform:

NOTE: There are a few errors in the Azure documentation:

- The password must be `Password1234!`.
- The username must be `plankton`.

- [AWS](https://learn.hashicorp.com/tutorials/terraform/aws-dependency?in=terraform/aws-get-started).
- [Azure](https://learn.hashicorp.com/tutorials/terraform/azure-dependency?in=terraform/azure-get-started).
- [GCP](https://learn.hashicorp.com/tutorials/terraform/google-cloud-platform-dependency?in=terraform/gcp-get-started).

# View the results

| [AWS Console](https://aws.amazon.com/console/) | [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups) | [GCP Console](https://console.cloud.google.com/) |

# Questions:

1. Does the order of resources in `main.tf` matter?
2. Where do dependecies between resources come from?
3. Can you explain what this means: `resource_group_name = azurerm_resource_group.rg.name`?
4. How can you express a list in [HCL](https://github.com/hashicorp/hcl)?
5. Can you login to the machine you've created?
6. Please change the machine to Ubuntu 18.04. (`sku = 18.04-LTS`)
7. Google for "terraform input sensitive". How can I set an environment variable to prevent me from typing (and seeing) the username and password?
