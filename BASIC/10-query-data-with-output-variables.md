# Querying data with output variables

|expected time|requirements                                    |
|-------------|------------------------------------------------|
|60 minutes   |A computer with Terraform installed, lab 9 done.|

## What?

Sometimes you want to know a detail of the infrastructure that Terraform built. This could be an IP address of some device for example.

For example, how do I know where to connect if I'm using this code:

```hcl
resource "digitalocean_ssh_key" "example" {
  name       = "example"
  public_key = file("id_rsa.pub")
}

resource "digitalocean_droplet" "web-1" {
  image  = "fedora-32-x64"
  name   = "web-1"
  region = "ams3"
  size   = "s-1vcpu-1gb"
  ssh_keys = [digitalocean_ssh_key.example.fingerprint]
}
```

You'll learn how Terraform

Learn how to define input variables:

- [AWS](https://learn.hashicorp.com/tutorials/terraform/aws-outputs?in=terraform/aws-get-started).
- [Azure](https://learn.hashicorp.com/tutorials/terraform/azure-outputs?in=terraform/azure-get-started).
- [GCP](https://learn.hashicorp.com/tutorials/terraform/google-cloud-platform-outputs?in=terraform/gcp-get-started).

# View the results

| [AWS Console](https://aws.amazon.com/console/) | [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups) | [GCP Console](https://console.cloud.google.com/) |

# Questions:

1. What is a typical value you'd like to see on `terraform apply`?
2. Would it not be simpler to output everything?
