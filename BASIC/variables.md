# Variables

There are a few location where you can set variables. Which location you choose depends a bit on the use case.

## Precendence

The variables can be overwritten, the ordering below. (Where the first item on the list is the weakest variable, overwritten by a variable lower in the list.

1. CLI (`-var`).
2. Specific variable files (`-var-file=`).
3. `*.auto.tfvars`.
4. terraform.tfvars
5. Environment variables (`TF_VAR_variable`).
6. root-module variables (`variable "identifier" { default="value" }`).
7. module variables (`variable "identifier" { default="value" }`).

## Locals or local variables

You can set variables that are only usable in the (root) module. For example, you could take a regulare variable, prefix or suffix and use the local variable.

```hcl
# You can define a mandatory input variable.
variable "name" {}

# now you define the local variable.
locals {
  default_name = "rg-${var.name}-sbx"
}

# Later you can reuse the local variable
resource "azurerm_resource_group" "rg" {
  name     = local.default_name
}
```

## Mapping values

You can define a map, and later lookup details from that map.

In `variables.tf` you can define:

```hcl
variable "sizes" {
  default = {
    small   = "Standard_DS1_v2"
    medium  = "Standard_DS2_v2"
    large   = "Standard_DS3_v2"
  }
}
```

In `main.tf` you can looup the variable:

```hcl
resource "azurerm_virtual_machine" "vm" {
  vm_size               = var.sizes["medium"]
  # This is similar, but uses `lookup`:
  # vm_size             = lookup(var.sizes, "medium")
```

In the example above a value of (literally) "medium" is used. That can also be a vvariable:

```hcl
variable "size" {
  default = "medium"
}

resource "azurerm_virtual_machine" "vm" {
  vm_size               = var.sizes[size]
```
