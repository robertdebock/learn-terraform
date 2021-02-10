# Solution 2

You module is ready to be used in your `learn-terraform-azure` repository.

1. Open main.tf
2. Find this block:

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rf-robertdebock-sbx"
  location = "west europe"
  tags = {
    Environment = "Terraform Getting Started"
    Team = "DevOps"
  }
}
```

3. Replace that block by this one:

```hcl
module "my_azurerm_resource_group" {
  source = "../../my_azurerm_resource_group/"
  name   = "test_rg"
  tags   = {
    Environment = "Terraform Getting Started"
    Team = "DevOps"
  }
}
```

NOTE: The `source` path (`../../`) depends on where your root-module and module are placed. This may need modification.

4. Run `terraform init` do "download" the module. (This module is local...)
5. Run `terraform plan`, and `terraform apply`.
