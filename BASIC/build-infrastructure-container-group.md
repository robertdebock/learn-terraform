# Build infrastructure container group

|expected time|requirements|
|-------------|------------|
| 60 minutes  | a computer |

Goal: Learn how to create Container Group resources on Azure using Terraform.

## Explanation

Azure can host containers for you, taking away the need to maintain your own infrastructure.

## Howto

Use [`azurerm_container_group`](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/container_group) to spin up a few containers.

## Demo

See [this example repository](https://github.com/robertdebock/terraform-azurerm-container-group).

## Assignment

- [ ] Use the example mentioned in the [documentation](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/container_group).

Once applied, the container group gets an IP address. (See the Azure portal)

The terraform code in the [documentation](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/container_group) show what port you may visit.

- [ ] Try to visit the IP address. (`https://IP_ADDRESS/`)

This does not work. Inspect the Azure Portal to understand what's wrong. (Hint below, but give yourself time to figure it out.)

- [ ] Fix the problem by changing the Terraform code.
- [ ] Apply again and try to visit the IP address.

You should now have a working website. Let's reduce the allocated memory and CPU, and likely [save a bit of money](https://azure.microsoft.com/en-us/pricing/details/container-instances/).

- [ ] Check in the [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups) how much memory the containers use.
- [ ] Change the `memory` parameter to `0.1` for both containers and apply the code.

## View the results

| [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups) |

## Questions

1. Do you see a use-case for your situation to use container groups?
2. Does each container have a unique IP-address?
3. What does your container group [cost](https://azure.microsoft.com/en-us/pricing/details/container-instances/) per month?

## Hints

- The port used in the Terraform code example is `443`, but the container just exposes `80`.
