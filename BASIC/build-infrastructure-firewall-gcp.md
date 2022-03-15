# Build infrastructure firewall

|expected time|requirements|
|-------------|------------|
| 30 minutes  | a computer |

Goal: Learn how to create GCP firewall using Terraform.

## Explanation

The `google_compute_firewall` provides a way to allow selected traffic.

## Howto

Read the [documentation](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_firewall). It's pretty straight forward.

## Demo

Have a look at this [example repository](https://github.com/robertdebock/terraform-gcp-firewall).

## Assignment

- [ ] Clone the [example repository](https://github.com/robertdebock/terraform-gcp-firewall) repository.
- [ ] Extend the `instance.tf` with an extra machine.
- [ ] Give both instances some tags, for example: "web" and "linux"
- [ ] Change `firewall.tf` to allow port `80` for instances with the tag `web`.
- [ ] Allow port `22` for machines with the tag `linux`.
- [ ] Allow `icmp` for any machine, from anywhere.

## Questions

1. Does this resource cost money?
2. Does this resource make a "stateful firewall"?
3. Could I ask a firewall administrator to add a rule to the firewall?
