# `remote-exec`

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|60 minutes   |A computer with Terraform installed, terraform knowledge.|

Goal: Be able to make use of `remote-exec` when required.

## Explanation

The `remote-exec` provisioner executes a command on the remote resource after creating the resource. This is typically applied when spinning up a machine, for example using `azurerm_virtual_machine`.

A few use-cases:

1. Install some package, enable some service, etc. (N.B. Disadvantages!)
2. Hook up a instance to some configuration management systems, for example [SaltStack](https://saltproject.io/).

Generally speaking; try to [limit](https://www.terraform.io/docs/language/resources/provisioners/syntax.html#provisioners-are-a-last-resort) the commands to the bare minimum to get going; there are better ways to configure a system.

For Azure virtual machines, there is also a resource [azurerm_virtual_machine_extension](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_machine_extension) which is more suitable to execute commands. Since most other cloud providers do not have such a resource, understanding `remote-exec` is quite useful.

## Howto

There are a few ways to execute commands on the remote host.

### inline

The `remote-exec` provisioner may need extra details on how to connect to the resource, you'll see them in the examples below.

These extra details include the `host`, which refers to the public ip address. In azure the public IP address is `azurerm_network_interface` resource, but only become available after the machine is created. Therefor a bit of dark magic is required: `depends_on`:

First, create a data block to find the IP address:

```hcl
data "azurerm_public_ip" "pip" {
  name                = azurerm_public_ip.pip.name
  resource_group_name = azurerm_resource_group.rg.name
  depends_on          = [azurerm_virtual_machine.vm, ]
}
```

Next let the `null_resource` depend on the block above:

For a (short list of) command(s), `inline` can be used.

```hcl
resource "null_resource" "default" {
  depends_on = [data.azurerm_public_ip.pip, ]
  connection {
    host     = data.azurerm_public_ip.pip.ip_address
    user     = "my_user"
    password = "Som3-P4s$W0rd."
  }
  provisioner "remote-exec" {
    inline = [
      "sudo apt-get update",
      "sudo apt-get upgrade -y"
      ]
  }
}
```

### script

When you need to run a single script, that likely contains many commands, you can use `script`. The script is copied to the remote resource and executed.

```hcl
resource "null_resource" "default" {
  depends_on = [data.azurerm_public_ip.pip, ]
  connection {
    host     = data.azurerm_public_ip.pip.ip_address
    user     = "my_user"
    password = "Som3-P4s$W0rd."
  }
  provisioner "remote-exec" {
    script = "my_script.sh"
  }
}
```

### scripts

If there are multiple scripts to be executed, `scripts` can be used:

```hcl
resource "null_resource" "default" {
  depends_on = [data.azurerm_public_ip.pip, ]
  connection {
    host     = data.azurerm_public_ip.pip.ip_address
    user     = "my_user"
    password = "Som3-P4s$W0rd."
  }
  provisioner "remote-exec" {
    scripts = [
      "my_script_1.sh",
      "my_script_2.sh"
    ]
  }
}
```

## Assignment

- [ ] Create a `azurerm_virtual_machine` and have update all packages. (Two commands: `sudo apt-get update` and `sudo apt-get upgrade -y`)
- [ ] Find out if the `null_resource` is stored in the state.

## Questions

1. Can you think of realistic use-cases?
2. Do you (in your organisation) use some kind of configuration management system?

## Solution

See [this repository](https://github.com/robertdebock/terraform-azurerm-remote-exec).

## Sources

- [remote-exec](https://www.terraform.io/docs/language/resources/provisioners/remote-exec.html)
