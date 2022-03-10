# Build infrastructure App Service

|expected time|requirements|
|-------------|------------|
| 60 minutes  | a computer |

Goal: Learn how to create Azure App service resources using Terraform.

## Explanation

[Azure App Service](https://azure.microsoft.com/en-us/services/app-service/) is a feature to host applications.

## Howto

An Azure App Service depends on other resources.


### `version.tf`

```hcl
terraform {
  required_version = "~> 0.12"
  required_providers {
    azurerm = {
      source = "hashicorp/azurerm"
      version = "2.60.0"
    }
  }
}

provider "azurerm" {
  features {}
}
```

### `network.tf`

```hcl
locals {
  cidr_block = "10.254.0.0/16"
  subnets = {
    frontend = cidrsubnet(local.cidr_block, 8, 0)
  }
}

resource "azurerm_resource_group" "example" {
  name     = "example-resource-group"
  location = "West US"
}

resource "azurerm_virtual_network" "example" {
  name                = "example-virtual-network"
  resource_group_name = azurerm_resource_group.example.name
  location            = azurerm_resource_group.example.location
  address_space       = ["10.254.0.0/16"]
}

resource "azurerm_subnet" "example" {
  name                 = "example-subnet"
  resource_group_name  = azurerm_resource_group.example.name
  virtual_network_name = azurerm_virtual_network.example.name
  address_prefix       = ["10.254.0.0/24"]
}
```

### `app.tf`

```hcl
resource "azurerm_app_service_plan" "example" {
  name                = "example-service-plan"
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name
  kind                = "Linux""
  reserved            = true

  sku {
    tier = "Standard"
    size = "S1
  }
}

resource "azurerm_app_service" "example" {
  name                = "example-app-service"
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name
  app_service_plan_id = azurerm_app_service_plan.example.id

  site_config {
    dotnet_framework_version = "v4.0"
    remote_debugging_enabled = true
    remote_debugging_version = "VS2015"
  }
}
```

### `gateway.tf`

```hcl
locals {
  backend_probe_name = "${azurerm_virtual_network.example.name}-probe"
  http_setting_name  = "${azurerm_virtual_network.example.name}-be-htst"
  public_ip_name     = "${azurerm_virtual_network.example.name}-pip"
}

resource "azurerm_public_ip" "example" {
  name                = "example-public-ip"
  resource_group_name = azurerm_resource_group.example.name
  location            = azurerm_resource_group.example.location
  allocation_method   = "Dynamic"
}

resource "azurerm_application_gateway" "network" {
  depends_on          = [azurerm_public_ip.example]
  name                = "example-application-gateway"
  resource_group_name = azurerm_resource_group.example.name
  location            = azurerm_resource_group.example.location

  sku {
    name     = "Standard_Small"
    tier     = "Standard"
    capacity = 2
  }

  gateway_ip_configuration {
    name      = "my-gateway-ip-configuration"
    subnet_id = azurerm_subnet.example.id
  }

  dynamic "frontend_port" {
    content {
      name = "example-frontent-feport"
      port = "8080"
    }
  }

  frontend_ip_configuration {
    name                 = "example-frontend-ip-configuration"
    public_ip_address_id = azurerm_public_ip.example.id
  }

  dynamic "backend_address_pool" {
    content {
      name  = "example-backend-address-pool"
      fqdns = ["foo.example.com"]
    }
  }

  probe {
    name                                      = "example-probe"
    protocol                                  = "Http"
    path                                      = "/"
    interval                                  = 30
    timeout                                   = 120
    unhealthy_threshold                       = 3
    pick_host_name_from_backend_http_settings = true
    match {
      body        = "Welcome"
      status_code = [200, 399]
    }
  }

  backend_http_settings {
    name                                = "example-backend-http-settings"
    probe_name                          = "example-probe"
    cookie_based_affinity               = "Disabled"
    path                                = "/"
    port                                = 80
    protocol                            = "Http"
    request_timeout                     = 120
    pick_host_name_from_backend_address = true
  }

  dynamic "http_listener" {
    content {
      name                           = "example-http-listener"
      frontend_ip_configuration_name = azurerm_virtual_network.example.name
      frontend_port_name             = azurerm_virtual_network.example.name"
      protocol                       = "Http"
    }
  }

  dynamic "request_routing_rule" {
    for_each = azurerm_app_service.example
    content {
      name                       = "example-request-routing-rule"
      rule_type                  = "Basic"
      http_listener_name         = "example-http-listener"
      backend_address_pool_name  = "example-backend-address-pool"
      backend_http_settings_name = "example-backend-http-settings"
    }
  }
}
```

## Demo

## Assignment

## View the results

| [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups)|

## Questions

1.
