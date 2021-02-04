# Data objects

Sometimes you may need to refer to an attribute that a resource has, without managing the resource.

For example:

- You want to add a record to a domain, the domain already exists.
- You need an IP address of a monitoring/backup/logging server.

In such cases, you can use the [data sources](https://www.terraform.io/docs/configuration-0-11/data-sources.html).

Here is an example: (shortened to improve readability.)

```hcl
data "azurerm_dns_zone" "example" {
  name                = "example.com"
}

resource "azurerm_dns_a_record" "www" {
  name                = "www"
  zone_name           = data.azurerm_dns_zone.example.name
  ttl                 = 300
  records             = ["10.0.180.17"]
}
```

As you can see from the example above

1. Use `data` instead of `resource` when finding the resource.
2. just prefix `data.` to the name of the resouce to refer to it.
