# Terragrunt

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|60 minutes   |A computer with terraform installed, terraform knowledge.|

Learn how to use [Terragrunt](https://terragrunt.gruntwork.io/).

## Explanation

Sometimes you've got an infrastructure coded that's almost identical for another environment. For example:

- Development, Test, Acceptance & Prodction
- Saas offerings; A wordpress website for multiple customers.
- Location based services; a CDN.

In those cases you can copy-paste a whole repository, change a few values and `apply` the terraform code. But what if you've copied such a repositories and you discover a flaw? You'd have to change multiple repositories to address the issue.

This is where [Terragrunt](https://terragrunt.gruntwork.io/) comes in. Terragrunt allows you to define the "logic" (all `resources` of an infrastructure) once and apply different settings for the different environments.

## Assignment

1. Take an example repository containing Terraform code and introduce Terragrunt so that you can use different values for "development" and "production".

## Questions

1. Do you see a purpose for Terragrunt in your organization?

## Solution

Have a look at [this (imperfect) repository](https://github.com/robertdebock/terragrunt-demo).
