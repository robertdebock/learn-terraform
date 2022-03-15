# Build infrastructure firewall

|expected time|requirements|
|-------------|------------|
| 30 minutes  | a computer |

Goal: Learn how to create Azure firewall using Terraform.

## Explanation

An [Azure firewall](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/firewall) offer unique characteristics like the [threat intel mode](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/firewall#threat_intel_mode). This can help securing a set of resources.

Have a look at the relations you can make:

~[Firewall dependencies](https://raw.githubusercontent.com/robertdebock/terraform-azurerm-firewall/master/graphviz.svg)

Be aware; experiments with an Azure Firewall can be expensive; the minimum amount of time for an Azure Firewall is 1 hour.

## Howto

There are quite some configurable parameters, but these resources are required:

- azurerm_resource_group
- azurerm_virtual_network
- azurerm_subnet
- azurerm_public_ip
- azurerm_firewall_policy
- azurerm_firewall_policy_rule_collection_group
- azurerm_firewall

## Demo

Have a look at this [Azure firewall module](https://github.com/robertdebock/terraform-azurerm-firewall).

There are many ways to configure an Azure firewall, your implementation likely differs.

## Assignment

- [ ] Clone the [Azure firewall module](https://github.com/robertdebock/terraform-azurerm-firewall) repository.
- [ ] Add a _scenario_ (under the examples `examples` directory).
- [ ] Customize some variables (see `variables.tf`).
- [ ] `plan`, `apply` and `destroy` your firewall.

## Questions

1. Where does the Azure Firewall differ from a [Network Security Group](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/network_security_group)?
2. What does a `Standard` and `Premium` Azure firewall cost per month?
