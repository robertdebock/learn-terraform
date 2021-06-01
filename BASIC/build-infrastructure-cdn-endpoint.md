# Build infrastructure CDN endpoint

|expected time|requirements|
|-------------|------------|
|60 minutes   |a computer  |

Goal: Learn how to create a CDN on Azure using Terraform.

## Explanation

A CDN (Content Delivery Network) is a service that can cache static content of a website, distributed globally. This service improves security and performance.

```text
\0/     +--- Azure CDN ---+      +--- Your website ---+
 | ---> |                 | ---> |                    |
/ \     +-----------------+      +--------------------+
```

## Howto

We'll use [`azurerm_cdn_endpoint`](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/cdn_endpoint) to play with the CDN service.

Be aware that it may take [90 minutes](https://docs.microsoft.com/en-us/azure/cdn/cdn-troubleshoot-endpoint) for the CDN to be propagated. Until that time you will see `404` errors. Once provisioned, changed take up to 90 minutes as well to propagate.

## Demo

See [this example repository](https://github.com/robertdebock/terraform-azurerm-cdn-endpoint).

## Assignment

- [ ] Copy-paste the example from the [documentation](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/cdn_endpoint).
- [ ] Change the `azurerm_cdn_profile.example.sku` to `Standard_Microsoft`.
- [ ] Modify the example to create a CDN for `https://xkcd.com/`. (`host_name`)
- [ ] Expose the this website under `https://YOUR_NAME.azureedge.net/`. (`azurerm_cdn_endpoint.example.name`)
- [ ] Visit https://YOUR_NAME.azureedge.net/.

Applying this code will take a while.

You can try other `host_name`s, depending on the configuration of the remote server, you may be returned a `502 Bad Gateway` error.

## Questions

1. Do you see a use-case for this in your environment?
