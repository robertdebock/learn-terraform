# Terraform Cloud

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|30 minutes   |A computer with Terraform installed, terraform knowledge.|

Goal: See how you can use Terraform Cloud.

## Explanation

[Terraform Cloud](https://app.terraform.io/) can help you manage remote state, locking and serve different variable per workspace. It also runs `terraform plan`, `terraform apply` and optionally `terraform destroy`.

Terraform Cloud is not required to run Terraform, but enabled easier collaboration.

There is a good [comparison table](https://www.terraform.io/docs/cloud/workspaces/index.html#workspace-contents) in the documentation.

In some environments, Terraform Cloud may need to manage resources via an API that's not available from the internet. In that case you may bring your own [Terraform Cloud Agent](https://www.terraform.io/docs/cloud/agents/index.html).

## Howto

Start with visiting [Terraform Cloud](https://app.terraform.io/).

## Demo

This [code](https://github.com/robertdebock/git-terraform-demo) is connected to this [Terraform Clould workspace](https://app.terraform.io/app/robertdebock/workspaces/git-terraform-demo).

## Assignment

There is a great [track](https://learn.hashicorp.com/collections/terraform/cloud-get-started) for this. That track covers much more than just workspaces, so i suggest to finish these labs:

- [ ] Sign up for Terraform Cloud
- [ ] Create a Workspace

The rest of the labs work with AWS, which is not always true for this course.

## Questions:

1. Name some benefits of Terraform Cloud over a local installation.
2. Where are variables stored when using Terraform Cloud?
3. You need to manage resources on an isolated network using Terraform Cloud, what can you use?

[Solutions](terraform-cloud-solutions).

## Sources

- [Terraform Cloud documentation](https://www.terraform.io/docs/cloud/workspaces/index.html)
