# Solution 1

There can be some differences, don't worry. This is what your module should look like.

## Files and directories

You should now have these files:

```
my_azurerm_resource_group/
├── examples (optional)
│   └── default (optional)
│       └── main.tf (optional)
├── main.tf
├── output.tf
└── variables.tf
```

The content of the files:

## variables.tf

```hcl
variable "name" {
  description = "A string for the name of the resource group."
}

variable "location" {
  description = "(Optional) A string for the location of the resource group."
  default = "west europe"
}

variable "tags" {
  description = "(Optional) A key-value map of tags for the resourcegroup."
  default = null
}
```

## main.tf

```hcl
resource "azurerm_resource_group" "rg" {
  name     = var.name
  location = var.location
  tags     = var.tags
}
```

## output.tf

```hcl
output "name" {
  description = "The name of the resource group."
  value       = azurerm_resource_group.rg.name
}

output "location" {
  description = "The location of the resource group."
  value       = azurerm_resource_group.rg.location
}

output "id" {
  description = "The id of the resource group."
  value       = azurerm_resource_group.rg.id
}

output "tags" {
  description = "The tags of the resource group."
  value       = azurerm_resource_group.rg.tags
}
```

## (optional) examples/default/main.tf

```hcl
module "my_azurerm_resource_group" {
  source   = "../../"
  name     = "test_rg"
  location = "west europe"
  tags     = {
    tag1 = "value1"
    tag2 = "value2"
  }
}

output "show-all-attributes" {
  value = module.my_azurerm_resource_group.*
}
```
