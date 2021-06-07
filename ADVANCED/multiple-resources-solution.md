# Multiple resource solutions

1. Tell Terraform how to authenticate.

```shell
export TF_VAR_checkly_api_key="your-api-key"
```

2. Pin the version of this provider.

Add this to `versions.tf`:

```hcl
terraform {
  required_providers {
    checkly = {
      source = "checkly/checkly"
      version = "0.8.1-rc2"
    }
  }
}
```

3. Add this to `providers.tf`:

```hcl
variable "checkly_api_key" {}

provider "checkly" {
  api_key = var.checkly_api_key
}
```

4. Add this to your `main.tf`, or create a new file, for example `checkly.tf`.

```hcl
resource "checkly_check" "example-check" {
  name                      = "Example check"
  type                      = "API"
  activated                 = true
  should_fail               = false
  frequency                 = 1
  double_check              = true
  ssl_check                 = true
  use_global_alert_settings = true

  locations = [
    "us-west-1"
  ]

  request {
    url              = "https://${azurerm_public_ip.publicip.ip_address}/"
    follow_redirects = true
    assertion {
      source     = "STATUS_CODE"
      comparison = "EQUALS"
      target     = "200"
    }
  }
}
```

5. Run `terraform init`, `terraform plan` and `terraform apply`.
