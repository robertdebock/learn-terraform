# Upgrading terraform

| expected time | requirements                                              |
|---------------|-----------------------------------------------------------|
| 15 minutes    | A computer with Terraform installed, terraform knowledge. |

Goal: Learn how to upgrade Terraform.

## Explanation

There are a couple of upgrades relevant when using Terraform:

- Terraform itself.
- Providers used in a repository.
- Modules used in a repository.

### Terraform

All versions of Terraform can be found on [releases.hashicorp.com](https://releases.hashicorp.com). Terraform is in the [terraform](https://releases.hashicorp.com/terraform/) directory.

When jumping versions, please review the [upgrade guide](https://www.terraform.io/language/upgrade-guides). This helps in understanding what changed, and if changes in your repository is required.

Typically you want to upgrade terraform and see if `terraform plan` still works.

### Providers

Providers also have a version. For example the [Terraform Google Cloud provider](https://registry.terraform.io/providers/hashicorp/google/latest/docs) has a version. This version can be found under the purple "USE PROVIDER" button.

You may not specify a version of the provider. That may give unstable results; `latest` will be used. Although the providers are quite flexible and deprecations usually are communicated well in advance; you can end up in a situation where the old version of the provider you are using will not work anymore.

Typically try to keep the providers up to date. Just as with any software; not updating for a long period of time may cause a difficult upgrade path.

### Modules

Very similar to providers; although some modules will not be maintained. These modules may stop working.

Any module has a version. Specifying the version to use makes your root-module more stable, but you may need to modify the version to ensure no deprecations occur.

## Howto


Here is an example of version pinning.

```hcl
terraform {
  required_version = "~> 1.1"
  required_providers {
    aws = {
      version = "~> 2.13.0"
    }
    random = {
      version = ">= 2.1.2"
    }
  }
}

module "vault" {
  source   = "robertdebock/vault/aws"
  version  = "3.0.1"
  variable = "value"
}
```

The upgrade of Terraform depends a bit on how the installation was done. In case packages are used, simply `apt-get update && apt-get upgrade terraform`, `yum update terraform`, and so on.

You can also place a binary in a path that's in your `PATH` variable to temporarily try a specific version. 
