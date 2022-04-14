# Best practices

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|90 minutes   |A computer with Terraform installed, terraform knowledge.|

Goal: Use the most common best practices

## Explanation

Let's go over a few best practices. Likey you/your company also has best practices. There is time to discuss these.

### Variables

- Use variables. Define them in `variables.tf`, assign them in [tfvars file](https://www.terraform.io/docs/configuration/variables.html#variable-definitions-tfvars-files), or set them in the environment.
- Set sensitive variables in [environment variables](https://www.terraform.io/docs/commands/environment-variables.html#tf_var_name).
- Use [Terragrunt](https://terragrunt.gruntwork.io/) for environmental differences. (Workspaces can also be used...)

### Dependencies

- Pin all used providers and modules in `versions.tf`.
- When writing modules, keep the dependency chain as flat/short as possible.
- For air-gapped installations, use [terraform-bundle](https://github.com/hashicorp/terraform/tree/master/tools/terraform-bundle) or refer to your local SCM.

### State

- Save the [state remotely](https://www.terraform.io/docs/state/remote.html).

### General

- Use variables for nearly all values. (In other words, write Terraform code like you are writing a Terraform module.)
- Use CI for modules. (and possibly releases)
- [`validate`](https://www.terraform.io/docs/commands/validate.html) and [format (`fmt`)](https://www.terraform.io/docs/commands/fmt.html) often.
- Terraform updates [frequently](https://releases.hashicorp.com/terraform/), read [release notes](https://github.com/hashicorp/terraform/blob/master/CHANGELOG.md). You can "watch" a repository in [github](https://github.com/hashicorp/terraform).
- Use modules over resources in your root repository.
- It's a good idea to treat all repositories like a module. (variables.tf, output.tf, version.tf)

### Modules

- Spend a good amount of time on a [README.md](https://www.makeareadme.com/).
- Suggest to use this order when writing new modules:
  1. `README.md` - Define the purpose of the module.
  2. `variables.tf` - Think about what to ask for.
  3. `locals.tf` - Your place to map "simple" variables to complex variables.""
  4. `output.tf` - Consider what to expose.
  5. `main.tf` - The "logic" for the module.
  7. `versions.tf` - Pin all dependencies.
  8. `providers.tf` - All provider specific configuration.
  9. `examples/*` - Try your module yourself.
  10. `LICENSE` - Yes, likely a pretty open one like Apache-2.0
  11. `.gitignore` - terraform.tfstate, terraform.tfstate.backup, .terraform

## Assignment

- [ ] Find as many improvements in this [example repository](https://github.com/robertdebock/terraform-demo/).

## Bonus assignment

- [ ] Make pull requests for the improvements.

## Questions

1. Do you know what to improve on your code now?
2. Do you use other practices worth sharing?

## Solution

See [here](best-practices-solution.md).
