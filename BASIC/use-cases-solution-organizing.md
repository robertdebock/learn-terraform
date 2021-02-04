# Organizing roles

You can define a "base" module that determines many values based on some input.

In this example we'll use a `env_shortcode` as the input. The `env_shortcode` refers to a three letter abbreviation that refers to the environment.

There are a limited number of valid values; in this example: 'dev' and 'prd'.

## Base module.

1. Create a directory `terraform-module-base` and step into the directory.
2. Create a file called `versions.tf`:

```hcl
# The `validation` of variables was introduced since Terraform 0.13."
terraform {
  required_version = ">= 0.13"
}
```

3. Create a file `variables.tf`:

```hcl
# This is the mapping beteween:
# - env_shortcode (left)
# - subscription (right)
variable "subscriptions" {
  type    = map
  default = {
    dev = "xyz-dev"
    prd = "abc-prd"
  }
}

# This is the required variable (string) to make the mapping.
variable "env_shortcode" {
  type    = string
  description = "The short (3 letter string) code for the environment. i.e. 'dev'."
  validation {
    condition     = contains(["dev", "prd"], var.env_shortcode)
    error_message = "Only 'dev' or 'prd' are supported."
  }
}

# This is a primitive variable, always returning "westeurope".
variable "location" {
  type    = string
  default = "westeurope"
}
```

4. Create a file `output.tf`:

```hcl
# To use variables generated in this module, you need to `output` them.

# Here the mapping is done between `subscriptions` and `env_shortcode`.
output "subscription" {
  value = var.subscriptions[var.env_shortcode]
}

# Here the location is returned.
output "location" {
  value = var.location
}
```

5. Try the module by running `terraform init` and `terraform apply`. You'll be asked for `env_shortcode`.

The base module is ready.

## A sub module.

Now that the base module is ready, you can use it from another module.

1. Create a directory `terraform-module-xyz` and step into the directory.
2. Create a file called `versions.tf`:

```hcl
# The `validation` of variables was introduced since Terraform 0.13."
terraform {
  required_version = ">= 0.13"
}

module "base-module" {
  source        = "../terraform-module-base"
  env_shortcode = "prd"
}
```

3. Create a file called `variables.tf`:

```hcl
variable "name" {
  description = "The name of something."
}
```

4. Create a file called `output.tf`:

```hcl
output "subscription" {
  value = module.base-module.subscription
}

output "location" {
  value = module.base-module.location
}

output "name" {
  value = var.name
}
```

Nota bene: this last step is just to show how the two roles work together, normally you would use the variables in `main.tf`.

5. Try the module by running `terraform init` and `terraform apply`. You'll be asked for `name`.

As you can see, the output show a mapped/calculated value for `subscription`:

```shell
$ terraform apply
var.name
  The name of something.

  Enter a value: my_name


An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:

Terraform will perform the following actions:

Plan: 0 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + location     = "westeurope"
  + name         = "my_name"
  + subscription = "abc-prd"

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes


Apply complete! Resources: 0 added, 0 changed, 0 destroyed.

Outputs:

location = "westeurope"
name = "my_name"
subscription = "abc-prd"
```
