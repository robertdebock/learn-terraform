# Build infrastructure

|expected time|requirements|
|-------------|------------|
|60 minutes   |a computer  |

Goal: Learn how to apply terraform code.

## Explanation

This is your first Terraform code. We'll start easy with a simple resource and build up from there.

In this lab Terraform will connect to a cloud provider for the first time, it will take a bit of setting up. There should be sufficient time to troubleshoot and debug issues.

## Howto

Let's build your first resources with Terraform, this does differ per provider.

- [AWS](https://learn.hashicorp.com/tutorials/terraform/aws-build?in=terraform/aws-get-started).
- [Azure](https://learn.hashicorp.com/tutorials/terraform/azure-build?in=terraform/azure-get-started).
- [GCP](https://learn.hashicorp.com/collections/terraform/gcp-get-started).

You'll likely have questions, don't hesitate to ask them.

To use a device code, issue:

```shell
az login --use-device-code
```

To use a specfic subscription, issue:

```shell
az account set --subscription x-y-z-a-b
```

## Demo

## Assignment

- [ ] Follow the instuction in the `Howto`, eventually you should be able to run `terraform apply` and see your results in the cloud providers console/portal.

## View the results

| [AWS Console](https://aws.amazon.com/console/) | [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups) | [GCP Console](https://console.cloud.google.com/) |

## Questions

1. If I have difficulties making some resource, can I manually create it?
2. Can you explain in your own words what `terraform init` does?
3. What are benefits (and drawbacks) of `terraform.tfstate`?
4. How many resources are in the example code below?

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rg-robertdebock-sbx"
  location = var.location
  tags = {
    Environment = "Terraform Getting Started"
    Team = "DevOps"
  }
}

# Create a virtual network
resource "azurerm_virtual_network" "vnet" {
    name                = "myTFVnet-robert"
    address_space       = ["10.0.0.0/16"]
    location            = var.location
    resource_group_name = azurerm_resource_group.rg.name
}

# Create subnet
resource "azurerm_subnet" "subnet" {
  name                 = "myTFSubnet-robert"
  resource_group_name  = azurerm_resource_group.rg.name
  virtual_network_name = azurerm_virtual_network.vnet.name
  address_prefixes     = ["10.0.1.0/24"]
}

# Create public IP
resource "azurerm_public_ip" "publicip" {
  name                = "myTFPublicIP-robert"
  location            = var.location
  resource_group_name = azurerm_resource_group.rg.name
  allocation_method   = "Static"
}

# Create Network Security Group and rule
resource "azurerm_network_security_group" "nsg" {
  name                = "myTFNSG-robert"
  location            = var.location
  resource_group_name = azurerm_resource_group.rg.name

  security_rule {
    name                       = "SSH"
    priority                   = 1001
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "22"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }
}

# Create network interface
resource "azurerm_network_interface" "nic" {
  name                      = "myNIC-robert"
  location                  = var.location
  resource_group_name       = azurerm_resource_group.rg.name

  ip_configuration {
    name                          = "myNICConfg-robert"
    subnet_id                     = azurerm_subnet.subnet.id
    private_ip_address_allocation = "dynamic"
    public_ip_address_id          = azurerm_public_ip.publicip.id
  }
}

# Create a Linux virtual machine
resource "azurerm_virtual_machine" "vm" {
  name                  = "myTFVM-robert"
  location              = var.location
  resource_group_name   = azurerm_resource_group.rg.name
  network_interface_ids = [azurerm_network_interface.nic.id]
  vm_size               = "Standard_DS1_v2"

  storage_os_disk {
    name              = "myOsDisk-robert"
    caching           = "ReadWrite"
    create_option     = "FromImage"
    managed_disk_type = "Premium_LRS"
  }

  storage_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = lookup(var.sku, var.location)
    version   = "latest"
  }

  os_profile {
    computer_name  = "myTFVM-robert"
    admin_username = var.admin_username
    admin_password = var.admin_password
  }

  os_profile_linux_config {
    disable_password_authentication = false
  }
}

data "azurerm_public_ip" "ip" {
  name                = azurerm_public_ip.publicip.name
  resource_group_name = azurerm_virtual_machine.vm.resource_group_name
  depends_on          = [azurerm_virtual_machine.vm]
}
```

5. (Trick question) An how many resources can you see here:

```hcl
module "my_module" {
  name = "robert"
}
```
