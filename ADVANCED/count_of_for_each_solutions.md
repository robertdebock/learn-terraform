# Assignment examples

## Solution to example 1

```hcl
resource "azurerm_resource_group" "example" {
  count    = 2
  name     = "example-${count.index}"
  location = "West Europe"
}
```

## Solution to example 2

```hcl
resource "azurerm_resource_group" "example" {
  for_each = toset( ["westeurope", "easteurope"] )
  name     = "example"
  location = each.value
}

```

## Solution to example 3

```hcl
resource "azurerm_resource_group" "example" {
  for_each = {
    my_first_resource_group = "westeurope"
    my_second_resource_group = "easteurope"
  }
  name     = each.key
  location = each.value
}
```
