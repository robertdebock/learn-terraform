# local values

| expected time | requirements                                              |
|---------------|-----------------------------------------------------------|
| 45 minutes    | A computer with Terraform installed, terraform knowledge. |

Goal: Be able to create and use `locals` to further abstract your data.

## Explanation

Sometimes using input [variables](https://www.terraform.io/docs/language/values/variables.html) is not enough. For example: imagine you want to ask a user for a `size`, which can be"

- `small`
- `medium`
- `large`

And where the deployment uses much more technical terms to indicate the [size](https://docs.microsoft.com/en-us/azure/virtual-machines/vm-naming-conventions). In that case, using a `locals` is a great way to map input variables to sizes.

You can also describe locals as variables that are not exposed; a user shouldn't/can't overwrite them. In situations where you refer to a certain value many times, you can place them in a local variable.

## Howto

Let's split up into a "simple" and "complex" example.

### Simple

You typically add locals to a new file, like `locals.tf`:

```hcl
locals {
  my_local = "xyz"
}
```

You can reuse these locals in your terraform code:

```hcl
resource "x" "default" {
  parameter = local.my_local
}
```

### More complicated

#### `locals.tf`

You can also use locals to lookup values and define data structures.

Here you define a map of data.

```hcl
locals {
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
    size      = local.azure_data_map[var.environment].size
  }
}
```

In the example above, you need variable called `environment` to map values.

#### `variables.tf`

```hcl
variable "environment" {
  type    = string
  default = "development"
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

## Assignment Azure

- [ ] Introduce `locals` to maps `size` to these values: Standard_A1_v2, Standard_A2_v2 or Standard_A4_v2 using the below starting point:

```hcl
variable "size" {
  description = "The size of the deployment."
  type        = string
  default     = "small"
  validation {
    condition     = contains(["small", "medium", "large"], var.size)
    error_message = "Please use \"small\", \"medium\" or \"large\"."
  }
}

resource "azurerm_virtual_machine" "default" {
  name    = "my_name"
  vm_size = "? FILL ME IN ?"
  ...
}
```

## Assignment GCP

- [ ] Start with [this example repository](https://github.com/robertdebock/terraform-gcp-database/blob/master/main.tf)

The is a value `tier = "db-f1-micro"` that needs to be simplified.

- [ ] Lookup available `tier`s [here](https://cloud.google.com/sql/docs/mysql/admin-api/rest/v1beta4/tiers/list?apix_params=%7B%22project%22%3A%22roberts-project-23%22%7D).

- [ ] Make a locals map:

| simple_name | tier name        | RAM (GB) |
|-------------|------------------|----------|
| small       |db-f1-micro       | 0.6      |
| medium      | db-n1-standard-2 | 8        |
| large       | db-n1-standard-4 | 16       |

- [ ] Make a variable "size" (or so), allowing "small", "medium" or "large".
- [ ] Lookup the tier name based on the variable.
- [ ] Modify the resource `google_sql_database_instance` to use your newly created local.

## Questions

1. What is the difference between `variable` and `locals`?

## Solution

```hcl
variable "size" {
  description = "The size of the deployment."
  type        = string
  default     = "small"
  validation {
    condition     = contains(["small", "medium", "large"], var.size)
    error_message = "Please use \"small\", \"medium\" or \"large\"."
  }
}

locals {
  _vm_sizes = {
    small  = "Standard_A1_v2"
    medium = "Standard_A2_v2"
    large  = "Standard_A4_v2"
  }
  vm_size = local._vm_sizes[var.size]
}

resource "azurerm_virtual_machine" "default" {
  name    = "my_name"
  vm_size = local.vm_size
  ...
}
```

## Sources

- [locals](https://www.terraform.io/docs/language/values/locals.html)
- [variables](https://www.terraform.io/docs/language/values/variables.html)
