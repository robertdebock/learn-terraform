# Destroy infrastructure

|expected time|requirements                                    |
|-------------|------------------------------------------------|
| 15 minutes  | A computer with Terraform installed.           |

Goal: Learn how to destroy infrastructure.

## Explanation

Specifically for tests is quick and simple to spin up new resources like virtual machines, loadbalancers, disks, etc. Once you're done with testing or developing, it's time to take the test infrastructure down again.

For production workloads is not common to `destroy` but rather change the `.tf` files and run `terraform apply` again.

## Howto

- [AWS](https://learn.hashicorp.com/tutorials/terraform/aws-destroy?in=terraform/aws-get-started).
- [Azure](https://learn.hashicorp.com/tutorials/terraform/azure-destroy?in=terraform/azure-get-started).
- [GCP](https://learn.hashicorp.com/tutorials/terraform/google-cloud-platform-destroy?in=terraform/gcp-get-started).

## Demo

## Assignment

- [ ] Remove all resources by running `terraform destroy`.

## View the results

| [AWS Console](https://aws.amazon.com/console/) | [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups) | [GCP Console](https://console.cloud.google.com/) |

## Questions

1. Now that you know how to destroy all resources defined, how do you destroy only one resource?
2. Why would you use `terraform destroy`?
3. Can you destroy without `terraform.tfstate` or `terraform.tfstate.backup`?

## Solution

Described in the `Howto`, specifically [here](https://learn.hashicorp.com/tutorials/terraform/azure-destroy?in=terraform/azure-get-started#destroy-your-infrastructure).
