# Multiple resource solutions

1. Tell Terraform how to authenticate.

```
export TF_VAR_checkly_api_key="your-api-key"
```

2. Pin the version of this provider.

Add this to `providers.tf` or `versions.tf`:

```
terraform {
  required_providers {
    checkly = {
      source = "checkly/checkly"
      version = "0.8.1-rc2"
    }
  }
}
```

3. Add this to your `main.tf`, or create a new file, for example `checkly.tf`.

```
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
