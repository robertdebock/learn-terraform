# Writing modules

|expected time|requirements                                     |
|-------------|-------------------------------------------------|
|60 minutes   |A computer with Terraform installed, lab 11 done.|

Goal: learn how to write Terraform modules.

## Explanation

You've learned how to write Terraform code. When you write code, you'll see that you will be [repeating](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) yourself. That can be a waste.
Modules to the rescue; with Terraform modules you can write (small) pieces of Terraform code that other (or yourself) can reuse. This prevents double code and makes maintaining your code much easier.

Imaging this example:

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rg-robertdebock-sbx"
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

There are a lot of double values in the example above:

1. The `name` has `robert` in it.
2. The `location` is set in both resources.

You can make a module where some of these values are set to a default value, so you can prevent naming them.

The benefit of using a module is that you can fix mistakes just once, (in the module) and you do not need to change your Terraform code that uses the module.

As you can see the `version = 1.0.0` is used. [Versioning](https://semver.org/) is important, you can indicate a few things:

1. The MAJOR version (`1`) indicates the compatibility. `2.0.0` is not compatible with `1.0.0`.
2. The MINOR version (`0`) indicates the features. If this number increases, a new feature should be available.
3. The PATCH version (`0`) indicates the bugfixes. If this number increases, a problem has been fixed.

Number can go beyond `9`, so a version a `3.2.13` is possible.

Many vendors do not use [SemVer](https://semver.org/), rather use a new version for marketing purposes.

## Howto

1. Make a new directory, maybe `terraform-module-azurerm-resource_group`.
2. Describe all input in `variables.tf`.
3. Describe all output in `outputs.tf`
4. Add a `README.md`.
5. Describe all resources in `main.tf`.
6. Describe all versions in `versions.tf`
7. Add `examples/default/main.tf` the uses the module.

- [HashiCorp teaches](https://learn.hashicorp.com/collections/terraform/modules).
- [Terraform modules](https://learn.hashicorp.com/tutorials/terraform/module-create?in=terraform/modules).

The [documentation](https://www.terraform.io/docs/modules/index.html) may also help.

## Demo

## Assignment

- [ ] Make a module that can create `azurerm_resource_group`s. [Solution](writing-modules-solution-1.md)
- [ ] Try your module by running `terraform init` from the `examples/default` directory.

## Bonus assignment

- [ ] Modify your root-module (`learn-terraform-azure`) to use the modules you've created. [Solution](writing-modules-solution-2.md)

## Best practices

1. Use [published modules](https://registry.terraform.io/browse/modules) when possible
2. Make modules as small as possible.
3. Use sane defaults. (for example `region` and `size`.)
4. Use no configuration in modules. (It should be usable by anybody.)
5. Use explicit variable names. (Not `r` but `region` for example.)
6. Create a `README.md` explaining the features.
7. Add a `LICENSE` before publishing.
8. Put `terraform.tfstate`, `terraform.tfstate.backup`, `.terraform` and `*.tfvars` in [`.gitignore`](https://github.com/github/gitignore/blob/master/Terraform.gitignore).

## Questions:

1. Why would you write a module?
2. Where can you find and download modules?
3. By looking at the downloads, what is the most used provider? (AWS, Azure or GCP)

## Extra

To use a module stored on a version control system, use this code:

```hcl
module "resourcegroup" {
  source              = "git::ssh://git@bitbucket.org/NAMESPACE/REPOSITORY.git"
  resource_group_name = local.resource_group_name
  location            = var.location
  rg_tags             = var.rg_tags
}
```
