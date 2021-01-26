# Build infrastructure

|expected time|requirements|
|-------------|------------|
|60 minutes   |a computer  |

# What?

This is your first Terraform code. We'll start easy with a simple resource and build up from there.

In this lab Terraform will connect to a cloud provider for the first time, it will take a bit of setting up. There should be sufficient time to troubleshoot and debug issues.

Let's build your first resources with Terraform, this does differ per provider.

- [AWS](https://learn.hashicorp.com/tutorials/terraform/aws-build?in=terraform/aws-get-started).
- [Azure](https://learn.hashicorp.com/tutorials/terraform/azure-build?in=terraform/azure-get-started).
- [GCP](https://learn.hashicorp.com/collections/terraform/gcp-get-started).

You'll likely have questions, don't hesitate to ask them.

To use a device code, issue:

```shell
az login --use-device-code
```

To use a specfic subscription, issue:

```shell
az account set --subscription x-y-z-a-b
```

# View the results

| [AWS Console](https://aws.amazon.com/console/) | [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups) | [GCP Console](https://console.cloud.google.com/) |

# Questions

1. If I have difficulties making some resource, can I manually create it?
2. Can you explain in your own words what `terraform init` does?
3. What are benefits (and drawbacks) of `terraform.tfstate`?
4. How many resources are in the example code below?

```
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

resource "digitalocean_droplet" "web-2" {
  image  = "fedora-32-x64"
  name   = "web-2"
  region = "ams3"
  size   = "s-1vcpu-1gb"
  ssh_keys = [digitalocean_ssh_key.example.fingerprint]
}

resource "digitalocean_loadbalancer" "web" {
  name   = "web"
  region = "ams3"

  forwarding_rule {
    entry_port     = 80
    entry_protocol = "http"

    target_port     = 80
    target_protocol = "http"
  }

  forwarding_rule {
    entry_port     = 443
    entry_protocol = "tcp"

    target_port     = 443
    target_protocol = "tcp"
  }

  healthcheck {
    port     = 22
    protocol = "tcp"
  }

  droplet_ids = [digitalocean_droplet.web-1.id, digitalocean_droplet.web-2.id,]
}
```

5. An how many resources can you see here:

```
module "digitalocean_droplet" {
  name = "my-droplet"
}
```
