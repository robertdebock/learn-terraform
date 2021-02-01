# Templates

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|60 minutes   |A computer with Terraform installed, terraform knowledge.|

Use Templates to customize your usage of Terraform.

## Explanation

Sometimes, you want Terraform to save a file with details from a Terraform run, such as an IP address. Terraform offers many [functions](https://www.terraform.io/docs/language/functions/index.html) one of which is the [templatefile function](https://www.terraform.io/docs/configuration/functions/templatefile.html).

## Howto

These templates can be used in (for example) [remote_file](https://registry.terraform.io/providers/mildred/sys/latest/docs/resources/file) or [local_file](https://registry.terraform.io/providers/hashicorp/local/latest/docs/resources/file).

Here is an example to store an IP address of hosts managed by Terraform:

`inventory.tf`:

```
resource "local_file" "inventory" {
    content  = templatefile("templates/inventory.tpl", { ip = data.azurerm_public_ip.ipaddress.ip_address })
    filename = "${path.module}/inventory"
}
```

`templates/inventory.tpl`:

```
${ip}
```

## Demo

## Assignment

You can start using [this Terraform configuration](https://github.com/hashicorp/learn-terraform-azure). (Remember: `az login`, `terraform init`)

- [ ] Please have Terraform write an ssh configuration listing the host managed by Terraform and sets the user to the user that's specified in the input variables. Use this format:

```
Host ${ip}
  User ${username}
```

## Questions:

1. How can you pin the version of `local_file`?
2. Do you know a use case for using templates?

## Conclusion

You can use generated content or input variables to create file, both locally and remote.

## Solution

- [Have a look at the steps](2-templates-solution.md).
- [Here is a repository with the code](https://github.com/robertdebock/learn-terraform-azure/tree/template).
