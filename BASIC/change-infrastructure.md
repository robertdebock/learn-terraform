# Change infrastructure

|expected time|requirements                                    |
|-------------|------------------------------------------------|
|15 minutes   |A computer with Terraform installed.            |

Goal Learn how to change infrastructure.

## Explanation

In the previous lab you were able to connect (and create a resource) on the cloud provider. Let's modify your code a bit and understand how Terraform reacts. You'll add a few tags to the `azurerm_resouce_group`.

## Howto

Follow the steps described below.

- [AWS](https://learn.hashicorp.com/tutorials/terraform/aws-change?in=terraform/aws-get-started).
- [Azure](https://learn.hashicorp.com/tutorials/terraform/azure-change?in=terraform/azure-get-started).
- [GCP](https://learn.hashicorp.com/tutorials/terraform/google-cloud-platform-change?in=terraform/gcp-get-started).

## Demo

- [GCP](https://github.com/robertdebock/learn-terraform-gcp/tree/change)

## Assignment

- [ ] Follow the step in the `Howto` section for your cloud provider.
- [ ] Make sure you run `terraform plan` and `terraform apply`.
- [ ] Verify in the cloud providers console/portal that your changes have been applied.

## View the results

| [AWS Console](https://aws.amazon.com/console/) | [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups) | [GCP Console](https://console.cloud.google.com/) |

## Questions:

1. Can I still change stuff (resources) manually on the providers console?
2. If I lost the state file, can I simply re-apply the same Terraform code?
3. If I change the name of an instance, will the instance be recreated or renamed?
4. Why would you append `-out=planfile` to `terraform plan`?

## Solution

It's described in this section:
- [Azure](https://learn.hashicorp.com/tutorials/terraform/azure-change?in=terraform/azure-get-started#update-your-configuration)
- [GCP](https://learn.hashicorp.com/tutorials/terraform/google-cloud-platform-change?in=terraform/gcp-get-started)
