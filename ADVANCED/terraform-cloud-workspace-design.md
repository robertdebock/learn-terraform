# Terraform Cloud workspace design

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|30 minutes   |A computer with Terraform installed, terraform knowledge.|

Goal: See how you can design workspaces in Terraform Cloud.

## Explanation

Terraform Cloud has a concept of "workspaces". A workspace is a bit like a directory or repository on you local computer, it contains state, variables, etc.

There are unique benefits to these workspaces, one of them is the offering and consumption of data from department to department.

Image a company with these departments:

- Networking - Deliving network services.
- Compute - Delivering compute services.

You can setup workspaces like this:

```text
+--- networking ------------+    +--- compute -------------------+
| azurerm_virtual_network   |    | azurerm_network_interface     |
| azurerm_subnet            | -> |   subnet_id                   |
| azurerm_public_ip         | -> |   public_ip_address_id        |
+---------------------------+    | azurerm_linux_virtual_machine |
                                 |  network_interface_ids        |
                                 +-------------------------------+
```

In the diagram above, the `compute` department needs two details from the `networking` department:

- `subnet_id`
- `public_ip_address_id`

This can be done by using a `data` object that points to another workspace:

```hcl
data "terraform_remote_state" "networking" {
  backend = "remote"

  config = {
    organization = "example"
    workspaces = {
      name = "networking"
    }
  }
}
```

You can use object from `data.terraform_remote_state.networking`:

```hcl
resource "azurerm_network_interface" "default" {
  name                = "my-network-interface"
  location            = "west europe"
  resource_group_name = "my-resource-group"

  ip_configuration {
    name                          = "my-ip-configuration"
    subnet_id                     = data.terraform_remote_state.networking.outputs.subnet_id
    private_ip_address_allocation = "dynamic"
  }
}
```

As you can see the `outputs` key is used, meaning the state referred to should have an `output` of `subnet_id`.

## Assignment

Take about 10 minutes to:

- [ ] Make a list of about 3 departments that either provide something to each other or consume somethign from another.
- [ ] Sketch (pseudo-code) what variables need to be used from a consumer.

Let's see what you came up with and if we can (re-)use a part of your design.

## Questions:

1. Does the model shown in the explanation fit your organization?

## Sources

- [`terraform_remote_state`](https://www.terraform.io/docs/language/state/remote-state-data.html).
- [MS CAF](https://github.com/Azure/caf-terraform-landingzones) may work for you.
