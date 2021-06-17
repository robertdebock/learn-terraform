# Build infrastructure DBAAS

|expected time|requirements|
|-------------|------------|
|60 minutes   |a computer  |

Goal: Learn how to create Azure dbaas resources using Terraform.

## Explanation

There are many Azure resources available, lets setup a managed MySQL instance.

## Howto

Using the [azurerm_mysql_server](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/mysql_server) and [azurerm_mysql_database](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/mysql_database) resources, we're going to create a managed MySQL instance.

## Demo

[Example code](https://github.com/robertdebock/terraform-azurerm-mysql-server)

## Assignment

Use the [sample code](https://github.com/robertdebock/terraform-azurerm-mysql-server) and change these settings:

- [ ] Set the `administrator_login` to 'my_admin'.
- [ ] Set the `administrator_login_password` to `my_passw0rd.`
- [ ] Use a size of 10 GB.

You'll likely run into an error. Try to understand the issue and fix the problem. (Hint: `name`.)

## View the results

| [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups)|

## Questions

1. What are valid choises for `version`?
2. What happens if I change the `version` to this resource?
3. Could I make a virtual machine and install MySQL myself?
