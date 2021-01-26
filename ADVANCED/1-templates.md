# Templates

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|60 minutes   |A computer with Terraform installed, terraform knowledge.|

Use Templates to customize your usage of Terraform.

## Explanation

Templates can be written using the [templatefile function](https://www.terraform.io/docs/configuration/functions/templatefile.html).

These templates can be reused in (for example) [remote_file](https://registry.terraform.io/providers/mildred/sys/latest/docs/resources/file) or [local_file](https://registry.terraform.io/providers/hashicorp/local/latest/docs/resources/file).

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

## Assignment

You can start using [this Terraform configuration](https://github.com/hashicorp/learn-terraform-azure). (Remember: `az login`, `terraform init`)

Please have Terraform write an ssh configuration listing the host managed by Terraform and sets the user to the user that's specified in the input variables.. Use this format:

```
Host ${ip}
  User ${username}
```

## Questions:

1. How can you pin the version of `local_file`?
2. Do you know a use case for using templates?

## Solution

[Have a look](1-templates-solution.md).
