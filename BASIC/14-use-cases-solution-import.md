# Importing resources

1. Add a resource group in the [Azure portal](https://portal.azure.com). I've called mine `MyRg`.
2. Add this to your `main.tf`:

```hcl
resource "azurerm_resource_group" "mine" {
  # (resource arguments)
}
```

3. Run `terraform import azurerm_resource_group.mine /subscriptions/1234abcd-12ab-23bc-34cd-abcdef112345/resourceGroups/MyRg`. The subscription can be obtained from the Azure Portal.

4. Run `terraform show` to see the results:

```hcl
# azurerm_resource_group.mine:
resource "azurerm_resource_group" "mine" {
    id       = "/subscriptions/c29870c1-9aff-4ac7-b431-a2f61e603891/resourceGroups/MyRg"
    location = "eastus"
    name     = "MyRg"
    tags     = {}

    timeouts {}
}
```

5. Paste this part into your `main.tf`.
