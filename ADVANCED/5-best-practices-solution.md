# Best practices solution

1. No modules are used, a direct reference to `resources` can be found in [do.tf](https://github.com/robertdebock/terraform-demo/blob/master/do.tf).
2. A `versions.tf` is missing, who knows if this code works with the current versions.
3. No CI has been configured.
4. The README.md suggests to use `terraform.tfvars` for sensitive variables.
5. Nothing is variable, `variables.tf` is missing.
6. No output is shown on `apply`. (`outputs.tf`)

Bonus: (In the `three` branch) An ssh-key in a public repository is never a good idea.
