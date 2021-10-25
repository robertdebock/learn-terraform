# Using multiple providers

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|120 minutes  |A computer with Terraform installed, terraform knowledge.|

Goal: Using multiple (related) resources and providers.

## Explanation

Sometimes you need to build infrastructure on more than 1 provider. Maybe you've got resources running on Azure and would like to add Cloudflare as a CDN.

Terraform can deal with multiple providers and basically becomes an [orchestrator](https://en.wikipedia.org/wiki/Orchestration_(computing)).

## Howto

### Multiple providers

When using multiple providers, it's time to move the `provider` block into it's own file, something like this:

`providers.tf`:

```hcl
terraform {
  required_version = ">= 0.13"
  required_providers {
    azurerm = {
      source = "hashicorp/azurerm"
      version = "2.45.1"
    }
    cloudflare = {
      source = "cloudflare/cloudflare"
      version = "2.13.2"
    }
  }
}

provider "azurerm" {
  features {}
}
```

### Refering

In Terraform you can refer to resources:

```
resource "azurerm_resource_group" "rg" {
  name     = "rf-robertdebock-sbx"
  location = "west europe"
}

# Create a virtual network
resource "azurerm_virtual_network" "vnet" {
    name                = "myTFVnet-robert"
    address_space       = ["10.0.0.0/16"]
    location            = "west europe"
    resource_group_name = azurerm_resource_group.rg.name
}
```

In the example above, the value of the parameter `resource_group_name` refers to `azurerm_resource_group.rg.name`.

You can also refer to resources hosted on different cloud providers:

```
resource "azurerm_public_ip" "publicip" {
  name                = "myTFPublicIP-robert"
  location            = "west europe"
  resource_group_name = azurerm_resource_group.rg.name
  allocation_method   = "Static"
}

resource "cloudflare_record" "foobar" {
  zone_id = "example.com"
  name    = "www"
  value   = azurerm_public_ip.publicip.ip_address
  type    = "A"
  ttl     = 3600
}
```

In the exampe above, the `azurerm_public_ip.publicip.ip_address` is used to configure a `cloudflare_record`.

There are [many providers](https://registry.terraform.io/browse/providers) that have something to offer.

### Multiple variants of the same provider

Sometimes you may need to create resources on one provider, but using different account or subscriptions. In such a case `alias` can be used uin the `provider` block:

```hcl
provider "azurerm" {
  features {}
}

provider "azurerm" {
  features {}
  alias       = "foo"
  environment = "german"
}

resource "azurerm_resource_group" "default" {
  name     = "something"
  location = "westeurope"
}

resource "azurerm_resource_group" "foo" {
  name     = "someotherthing"
  location = "westeurope"
  provider = azurerm.foo
}
```

The example above use the `german` `environment` and can be use by adding `provider = NAME`.

## Assignment

- [ ] In the Terraform code that you have, add a [checkly](https://www.checklyhq.com/) resource to monitor your instance. Use references to named values to dynamically configure checkly.
- [ ] If time permits it, experiment with the [uptime robot status page](https://registry.terraform.io/providers/louy/uptimerobot/latest/docs).

You need to sign-up to checkly. You can use your github account or email.

## Questions

1. Browse through [the registry](https://registry.terraform.io/browse/providers). Do you see any providers that could help you?

## Solution

- [Here you go](multiple-resources-solution.md).
- A [example repository, branch `checkly`](https://github.com/robertdebock/learn-terraform-azure/tree/checkly).
