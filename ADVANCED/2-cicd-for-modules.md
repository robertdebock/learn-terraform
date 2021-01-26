# CI/CD for modules

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|60 minutes   |A computer with Terraform installed, terraform knowledge.|

Setup CI/CD for Terraform modules.

## Explanation

Testing help you to keep your modules in a good state and makes it easier to contribute.

A discussion before we begin: "What can we test of a Terraform module?" ([Possible-answers](2-cicd-for-modules-test.md))

## Assignment

For your version control system, write a CI/CD file that tests a module. The tests may be simple, they can be extended later.

This may take some time, but it's well worth the effort as these pipelines will run quite frequently.

With CI/CD, always start with the smallest unit/component. This ensures you can deliver value incrementally instead of a "waterfall" approach.

## Questions

1. Would you `terraform apply` the code in CI when testing a module?
2. If you would `terraform apply`, how would you make sure `terraform destroy` runs whatever the output of `terraform apply`.

## Solution

- A [GitLab](2-cicd-for-modules-gitlab.yml)
- A [GitHub Action](https://github.com/robertdebock/terraform-action).
