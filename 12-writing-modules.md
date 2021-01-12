# Writing modules

|expected time|requirements                                     |
|-------------|-------------------------------------------------|
|60 minutes   |A computer with terraform installed, lab 11 done.|

Learn how to write Terraform modules:

[HashiCorp teaches](https://learn.hashicorp.com/collections/terraform/modules) [Terraform modules](https://learn.hashicorp.com/tutorials/terraform/module-create?in=terraform/modules).

The [documentation](https://www.terraform.io/docs/modules/index.html) may also help.

## Best practices

1. Use [published modules](https://registry.terraform.io/browse/modules) when possible
2. Make modules as small as possible.
3. Use sane defaults. (for example `region` and `size`.)
4. Use no configuration in modules. (It should be usable by anybody.)
5. Use explicit variable names. (Not `r` but `region` for example.)
6. Create a `README.md` explaining the features.
7. Add a `LICENSE` before publishing.
8. Put `terraform.tfstate`, `terraform.tfstate.backup`, `.terraform` and `*.tfvars` in [`.gitignore`](https://github.com/github/gitignore/blob/master/Terraform.gitignore).
9. 

# Questions:

1. Why would you write a module?
2. Where can you find and download modules?
3. By looking at the downloads, what is the most used provider? (AWS, Azure or GCP)
