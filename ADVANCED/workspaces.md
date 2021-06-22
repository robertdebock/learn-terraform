# Workspaces

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|30 minutes   |A computer with Terraform installed, terraform knowledge.|

Goal: Get familiar with Terraform workspaces.

## Explanation

Terraform [workspaces](https://www.terraform.io/docs/language/state/workspaces.html) can be used create different locations to store state. It also introduces an extra variable: `terraform.workspace`.

You're always working in a workspace, but if you do no select one, you're in teh `default` workspace.

## Howto

The arguments can be either of `new`, `select`, `list`, `delete` or `show`.

```
terraform workspace new my_workspace
terraform workspace select default
terraform workspace list
terraform workspace delete my_workspace
```

## Demo

See [this repo](https://github.com/robertdebock/terraform-azurerm-workspaces).

## Assignment

- [ ] From an existing repository, create a new workspace.
- [ ] Reuse the `terraform.workspace` variable to change the `name` of a resource.
- [ ] Map the workspaces to a parameter of the resource, like `location` or `size`. (locals.tf)

## Questions:

1. What are [good use-cases](https://www.terraform.io/docs/language/state/workspaces.html#when-to-use-multiple-workspaces)?
2. Do you see where you could apply this in your situation?
