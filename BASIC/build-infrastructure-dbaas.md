# Build infrastructure

|expected time|requirements|
|-------------|------------|
|60 minutes   |a computer  |

Goal: Learn how to create Azure dbaas resources using Terraform.

## Explanation

There are many Azure resources available, lets setup a managed MySQL instance.

## Howto

Using the [azurerm_mysql_server](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/mysql_server) resource, we're going to create a managed MySQL instance.

```hcl
resource "azurerm_resource_group" "example" {
  name     = "example-resources"
  location = "West Europe"
}

resource "azurerm_mysql_server" "example" {
  name                = "example-mysqlserver"
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name

  administrator_login          = "mysqladminun"
  administrator_login_password = "H@Sh1CoR3!"

  sku_name   = "B_Gen5_2"
  storage_mb = 5120
  version    = "5.7"

  auto_grow_enabled                 = true
  backup_retention_days             = 7
  geo_redundant_backup_enabled      = false
  infrastructure_encryption_enabled = true
  public_network_access_enabled     = true
  ssl_enforcement_enabled           = true
  ssl_minimal_tls_version_enforced  = "TLS1_2"
}
```

## Demo

## Assignment

Use the sample code above and change these settings:

- [ ] Set the `administrator_login` to 'my_admin'.
- [ ] Set the `administrator_login_password` to `my_passw0rd.`
- [ ] Use a size of 10 GB.

## View the results

| [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups)|

## Questions

1. What are valid choises for `version`?
2. What happens if I change the `version` to this resource?
3. Could I make a virtual machine and install MySQL myself?
