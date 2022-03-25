# Output

| expected time | requirements                                   |
|---------------|------------------------------------------------|
| 30 minutes    | A computer with Terraform installed.           |

Goal: Understand how output can displayed.

## Explanation

![input output](images/input-output.png "Input Output")

The command `terraform show` will display everything that Terraform knows. It basically dumps the state. All that output may be a little too much, so you may want to output specific values. Think of:

- An IP address of the load balancer.
- An instruction what to do next.
- The DNS name of the websites that Terraform deployed.

## Howto

You can specify Terraform to show output. Mostly these outputs are stored in `outputs.tf`, sometimes the output is specified in a function-specific file, such as `networking.tf` or `instances.tf`.

```hcl
output "ip_addr" {
  value       = google_comput_instance.default.network_interface.0.access_config.0.nat_ip
  description = "The public NAT ip address of the instance."
}
```

If a Terraform module specifies output, that output may be used elsewhere:

```hcl
resource "fake" "default" {
  name    = "www"
  ip_addr = module.THE_NAME_OF_THE_MODULE.ip_addr
}
```

There is an attribute `sensitive`. This indicates that Terraform should not show the sensitive information as output, but other modules or resources can use the item.

You may add `depends_on` list to indicate that Terraform should first create items in the list before showing the information.

You can use functions to transform the output.

## Demo

- See [this Azure file](https://github.com/robertdebock/learn-terraform-azure/blob/master/outputs.tf).
- See [this GCP file](https://github.com/robertdebock/terraform-gcp-output/blob/master/output.tf)

## Assignment

- In one of your directories/repositories that you already have, add an `output` attribute.
- Show `"Hello world!"` as output.
- Use a function to show `["Hello world!"]`.

# Questions:

1. Does adding `sensitive = true` parameter make data fully safe?
