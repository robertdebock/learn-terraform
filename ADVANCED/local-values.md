# local values

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|45 minutes   |A computer with Terraform installed, terraform knowledge.|

Goal: Be able to create and use `locals` to further abstract your data.

## Explanation

Sometimes using input [variables](https://www.terraform.io/docs/language/values/variables.html) are not enough. For example: imagine you want to ask a user for a `size`, which can be"

- `small`
- `medium`
- `large`

And where the deployment uses much more technical terms to indicate the [size(https://docs.microsoft.com/en-us/azure/virtual-machines/vm-naming-conventions)]. In that case, using a `locals` is a great way to map input variables to sizes.

You can also describe locals as variables that are not exposed; a user can't overwrite them. In situations where you refer to a certain value many times, you can place them in a local variable.

## Howto

Let's split up into a "simple" and "complex" example.

### Simple

You typically add locals to a new file, like `locals.tf`:

```hcl
locals {
  my_prefix = "rg"
}
```

You can reuse these variables in your terraform code:

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "${local.my_prefix}_robert"
  location = "westeurope"
}
```

This will result in a `name` of `rg_robert`.

### More complicated

#### `locals.tf`

You can also use locals to lookup values and define data structures.

Here you define a map of data.

```hcl
azure_data_map = {
  development = {
    location = "West Europe"
    size     = "small"
  }
  production = {
    location = "Central US"
    size     = "medium"
  }

  location  = local.azure_data_map[var.environment].location
  size      = local.azure.data_map[var.environment].size
}
```

In the example above, you need variable called `environment` to map values.

#### `variables.tf`

```hcl
variable "environment" {
  type    = string
  default = "West Europe"
  validation {
    condition     = contains(["development", "production"])
    error_message = "Please use "development" or "production" for the environment."
  }
}
```

Now you can simply call `local.location` or `local.size` in your `main.tf`. (Or anywhere else...)

#### `main.tf`

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rg-robertdebock-sbx"
  location = local.location
}
```

## Assignment

- [ ] Introduce `locals` to prevent duplicate code to the example below:

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rg-robertdebock-test"
  location = "westeurope"
}

resource "azurerm_virtual_network" "vnet" {
  name                = "vnet-robertdebock-test"
  address_space       = ["10.0.0.0/16"]
  location            = "westeurope"
  resource_group_name = azurerm_resource_group.rg.name
}
```

These values contain duplicates:

- The `location` is always `westeurope`.
- Both `name` values of `azurerm_resource_group` and `azurerm_virtual_network` contain `robertdebock`.
- Both `name` values of `azurerm_resource_group` and `azurerm_virtual_network` end with `test`.


## Questions

1. What is the difference between `variable` and `locals`?

## Solution

```hcl
locals {
  my_location    = "westeurope"
  my_name        = "robertebock"
  my_environment = "test"
}

resource "azurerm_resource_group" "rg" {
  name     = "rg-${local.my_name}-${local.environment}"
  location = local.my_location
}

resource "azurerm_virtual_network" "vnet" {
  name                = "vnet-${local.my_name}-${local.environment}"
  address_space       = ["10.0.0.0/16"]
  location            = local.my_location
  resource_group_name = azurerm_resource_group.rg.name
}
```

## Sources

- [locals](https://www.terraform.io/docs/language/values/locals.html)
- [varialbe](https://www.terraform.io/docs/language/values/variables.html)
