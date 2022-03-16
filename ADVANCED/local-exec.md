# `local-exec`

| expected time | requirements                                              |
|---------------|-----------------------------------------------------------|
| 30 minutes    | A computer with Terraform installed, terraform knowledge. |

Goal: Know when and how to use the `local-exec` provisioner.

## Explanation

The `local-exec` provisioner executes a command right after creating a resource.

A few use-cases:

1. Add a detail of the resource to a list. (See example above.)
2. Add a machines (ip or hostname) to an inventory so Ansible can use it.
3. Add a resource to the CMDB.
4. Start a configuration management system for that host.

Using local-exec has a few drawbacks, so use it when there is no other solution.

## Howto

The example below adds a line to `resource_groups.txt` when the creation of the resource group is done.

```hcl
resource "azurerm_resource_group" "example" {
  name     = "example"
  location = "West Europe"
  provisioner "local-exec" {
    command = "echo ${self.name} >> resource_groups.txt"
  }
}
```

## Assignment

- [ ] Use the `local-exec` provisioner to write an IP-address into a file for this Terraform code.

For Azure you will need to use the [documentation for azurerm_network_interface](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/network_interface) to get the `private_ip_address`.

### Azure

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rg-robertdebock-sbx"
  location = "westeurope"
}

resource "azurerm_virtual_network" "vnet" {
    name                = "myTFVnet-robert"
    address_space       = ["10.0.0.0/16"]
    location            = azurerm_resource_group.rg.location
    resource_group_name = azurerm_resource_group.rg.name
}

resource "azurerm_subnet" "subnet" {
  name                 = "myTFSubnet-robert"
  resource_group_name  = azurerm_resource_group.rg.name
  virtual_network_name = azurerm_virtual_network.vnet.name
  address_prefixes     = ["10.0.1.0/24"]
}

resource "azurerm_network_interface" "nic" {
  name                      = "myNIC-robert"
  location                  = azurerm_resource_group.rg.location
  resource_group_name       = azurerm_resource_group.rg.name

  ip_configuration {
    name                          = "myNICConfg-robert"
    subnet_id                     = azurerm_subnet.subnet.id
    private_ip_address_allocation = "dynamic"
  }
}

resource "azurerm_virtual_machine" "vm" {
  name                  = "myTFVM-robert"
  location              = azurerm_resource_group.rg.location
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
    sku       = "16.04-LTS"
    version   = "latest"
  }

  os_profile {
    computer_name  = "myTFVM-robert"
    admin_username = "my_admin"
    admin_password = "Som3-P4s$W0rd."
  }

  os_profile_linux_config {
    disable_password_authentication = false
  }
}
```

### GCP

```hcl
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "4.13.0"
    }
  }
}

provider "google" {
  # Change this for your project.
  project = "roberts-project-23"
  region  = "us-central1"
}

resource "google_compute_instance" "default" {
  name         = "default"
  machine_type = "e2-medium"
  zone         = "us-central1-a"
  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-9"
    }
  }
  network_interface {
    network = "default"
    access_config {}
  }
  metadata = {
    # This required a file called id_rsa.pub.
    ssh-keys = "username:${file("id_rsa.pub")}"
  }
}
```

## Questions

1. Will the `local-exec` provisioner run again when running `terraform apply`?
2. If I change a detail in `azurerm_network_interface` or `network_interface`, will the `local-exec` provisioner run again?
3. Is the `local-exec` provisioner stored in the state?
4. What are drawbacks of using `local-exec`?
5. What are alternatives for `local-exec`?

## Solution Azure

```hcl
# skipped a few resources

resource "azurerm_network_interface" "nic" {
  name                      = "myNIC-robert"
  location                  = azurerm_resource_group.rg.location
  resource_group_name       = azurerm_resource_group.rg.name

  ip_configuration {
    name                          = "myNICConfg-robert"
    subnet_id                     = azurerm_subnet.subnet.id
    private_ip_address_allocation = "dynamic"
  }
  provisioner "local-exec" {
    command = "echo ${self.private_ip_address} >> my_file.txt"
  }
}

# skipped a few resources
```

## Solution GCP

```hcl
# skipped a few resources

resource "google_compute_instance" "default" {
  name         = "default"
  machine_type = "e2-medium"
  zone         = "us-central1-a"
  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-9"
    }
  }
  network_interface {
    network = "default"
    access_config {}
  }
  metadata = {
    # This required a file called id_rsa.pub.
    ssh-keys = "username:${file("id_rsa.pub")}"
  }

  provisioner "local-exec" {
    command = "echo ${self.google_compute_instance.proxy.network_interface[0].access_config[0].nat_ip} >> my_file.txt"
  }

}

# skipped a few resources
```

## Sources

- [local-exec](https://www.terraform.io/docs/language/resources/provisioners/local-exec.html)
