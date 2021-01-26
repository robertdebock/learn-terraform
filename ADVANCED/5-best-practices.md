# Best practices

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|90 minutes   |A computer with Terraform installed, terraform knowledge.|

Use the most common best practices

## Explanation

### Variables

- Put variables in a [tfvars file](https://www.terraform.io/docs/configuration/variables.html#variable-definitions-tfvars-files).
- Set sensitive variables in [environment variables](https://www.terraform.io/docs/commands/environment-variables.html#tf_var_name).
- Use [Terragrunt](https://terragrunt.gruntwork.io/) for environment differences.

### Dependencies

- Pin all used providers and modules in `versions.tf`.
- For air-gapped installations, use [terraform-bundle](https://github.com/hashicorp/terraform/tree/master/tools/terraform-bundle).

### State

- Save the [state remotely](https://www.terraform.io/docs/state/remote.html).

### General

- Use variables for nearly every value.
- Use CI for modules and releases.
- [`validate`](https://www.terraform.io/docs/commands/validate.html) and [format (`fmt`)](https://www.terraform.io/docs/commands/fmt.html) often.
- Terraform updates [frequently](https://www.terraform.io/docs/commands/fmt.html), read [release notes](https://github.com/hashicorp/terraform/blob/master/CHANGELOG.md).
- Use modules over resources.
- It's a good idea to treat all repositories like a module. (variables.tf, output.tf, version.tf)

### Modules

- Spend a good amount of time on a [README.md](https://www.makeareadme.com/).
- Use this order when writing new modules:
  1. README.md - Define the purpose of the module.
  2. variables.tf - Think about what to ask for.
  3. output.tf. - Consider what to expose.
  4. main.tf. - The "logic" for the module.
  5. versions.tf - Pin all dependencies.
  6. examples/* - Try your module yourself.
  7. LICENSE - Yes, likely a pretty open one like Apache-2.0
  8. .gitignore - terraform.tfstate, terraform.tfstate.backup, .terraform

## Assignment

Find as many improvements in this [example repository](https://github.com/robertdebock/terraform-demo/).

Bonus: make pull requests for the improvements.

## Questions

1. Do you know what to improve on your code now?
2. Do you use other practices worth sharing?

## Solution

See [here].
