# Build a CDN.

|expected time|requirements|
|-------------|------------|
| 60 minutes  | a computer |

Goal: Learn how to create a CDN on GCP using Terraform.

## Explanation

A CDN (Content Delivery Network) is a service that can cache static content of a website, distributed globally. This service improves security and performance.

```text
\0/     +--- GCP CDN -----+      +--- Your website ---+
 | ---> |                 | ---> |                    |
/ \     +-----------------+      +--------------------+
```

## Howto

We'll use these resources to setup a CDN:

- google_compute_network
- google_compute_subnetwork
- google_compute_global_address
- google_compute_global_forwarding_rule
- google_compute_target_http_proxy
- google_compute_url_map
- google_compute_backend_service
- google_compute_instance_template
- google_compute_health_check
- google_compute_instance_group_manager
- google_compute_firewall

## Demo

See [this example repository](https://github.com/robertdebock/terraform-gcp-cdn).

## Assignment

- [ ] Start with the [example](https://github.com/robertdebock/terraform-gcp-cdn) repository.
- [ ] Add "Hello world" to the `index.html`.
- [ ] Run `terraform apply`.
- [ ] Run `ab -n 1024 -c 16 http://{{ IP-ADDRESS }}` to measure the response times.

## Questions

1. Do you see a use-case for this in your environment?
