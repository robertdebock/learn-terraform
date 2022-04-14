# Terragrunt

| expected time | requirements                                             |
|---------------|----------------------------------------------------------|
| 90 minutes    |A computer with Terraform installed, terraform knowledge. |

Goal: Learn how to use [Terragrunt](https://terragrunt.gruntwork.io/).

## Explanation

![terragrunt overview](images/key-features-terraform-code-dry.png "Terragrunt overview")

Sometimes you've got an infrastructure coded that's almost identical for another environment. For example:

- Development, Test, Acceptance & Prodction
- Saas offerings; A wordpress website for multiple customers.
- Location based services; a CDN.

In those cases you can copy-paste a whole repository, change a few values and `apply` the terraform code. But what if you've copied such a repositories many times and you discover a flaw? You'd have to change multiple repositories to address the issue.

This is where [Terragrunt](https://terragrunt.gruntwork.io/) comes in. Terragrunt allows you to define the "logic" (all `resources` of an infrastructure) once and apply different settings for the different environments. (Actually terragrunt can also manage [backends](https://terragrunt.gruntwork.io/docs/getting-started/quick-start/#keep-your-backend-configuration-dry), [cli arguments](https://terragrunt.gruntwork.io/docs/getting-started/quick-start/#keep-your-terraform-cli-arguments-dry) and [more](https://terragrunt.gruntwork.io/).

## Howto

We'll focus one managing terraform code with Terragrunt. Terragrunt (not by HashiCorp by the way) uses this filestructure:

```
.
├── modules             # This contains (almost) normal Terraform code.
│   ├── main.tf
│   ├── providers.tf
│   └── versions.tf
├── development         # This contains the specific settings for development.
│   └── terragrunt.hcl
├── production          # This contains the specific settings for production.
│   └── terragrunt.hcl
└── README.md
```

The files `development/terragrunt.hcl` and `production/terragrunt.hcl` look quite similar, here is one:

```hcl
terraform {
  source = "../modules"
}

inputs = {
  amount = 1
  size   = "s-1vcpu-1gb"
  name   = "development"
}
```

(Where the `inputs` change per environment.)

The file `modules/variables.tf` (or any .tf file) can pickup the variables set by terragrunt:

```
variable "amount" {
  description = "The number of instances to create."
}

variable "size" {
  description = "The size of the instance(s) to create."
}

variable "name" {
  description = "The name of the instance(s) to create."
}
```

You can set `default` values. In that case you may omit the variable in `terragrunt.hcl`.

With those files, it's time to create infrastructure.

1. `cd` into `production`.
2. Run `terragrunt init` to download dependencies. (Optional step, `terragrunt plan` initialized when required.)
3. Run `terragrunt plan`.
4. Run `terragrunt apply`.
5. Finally run `terragrunt destroy`.

## Demo

Have a [look](https://github.com/robertdebock/terragrunt-demo).

## Assignment

1. Take any directory containing Terraform code with a variable.
2. Introduce Terragrunt so that you can use different values for different environments. You could create "development" & "production" or "belgium" & "germany". (Or use a separation that applies to your company.)
3. Have a different `environment` or `location`.

When going into the folders containing `terragrunt.hcl`, try `terragrunt apply`.

## Questions

1. Do you see a purpose for Terragrunt in your organization?
2. Do you see resources that require a change if you'd like to deploy multiple of them?
3. In [this terragrunt repositor](https://github.com/robertdebock/learn-terraform-azure/tree/terragrunt), can I run `terragrunt init && terragrunt apply` in both `applicationX` and `applicationY`?

## Solution

- Have a look at [this (imperfect) repository](https://github.com/robertdebock/terragrunt-demo) for inspiration.
- The solution is in the [terragrunt branch](https://github.com/robertdebock/learn-terraform-azure/tree/terragrunt).
