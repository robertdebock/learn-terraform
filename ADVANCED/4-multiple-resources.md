# Using multiple resources and providers

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|120 minutes  |A computer with terraform installed, terraform knowledge.|

Using multiple (relates) resources and providers.

## Explanation

In Terraform you can refer to resources:

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
```

You can also refer to resources hosted on different cloud providers:

```
resource "digitalocean_droplet" "web-1" {
  image  = "fedora-32-x64"
  name   = "web-1"
  region = "ams3"
  size   = "s-1vcpu-1gb"   
}

resource "cloudflare_record" "foobar" {
  zone_id = "example.com"
  name    = "www"
  value   = digitalocean_droplet.web-1.ipv4_address
  type    = "A"
  ttl     = 3600
}
```

## Assignment

In the Terraform code that you have, add a [checkly](https://www.checklyhq.com/) resource to monitor your instance. Uses references to named values.

You need to sign-up to checkly. You can use your github account or email.

## Questions

1. The second example can be improved, do you see how?

## Solution

[Here you go](4-multiple-resources-solution.md).
