# Writing modules

|expected time|requirements                                     |
|-------------|-------------------------------------------------|
|60 minutes   |A computer with Terraform installed, lab 11 done.|

## What?

You've learned how to write Terraform code. When you write code, you'll see that you will be [repeating](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) yourself. That can be a waste.
Modules to the rescue; with Terraform modules you can write (small) pieces of Terraform code that other (or yourself) can reuse. This prevents double code and makes maintaining your code much easier.

Imaging this example:

```hcl
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
```

There are a lot of double values in the example above:

1. The `image`.
2. The `name` is almost identical.
3. The `region`.
4. The `size`.
5. The `ssh_keys`.

You can make a module where some of these values are set to a default value, so you can prevent naming them.

We'll work on writing modules so that you can reduce the example above to something like this:

```hcl
module "droplet" {
  source  = "robertdebock/droplet/digitalocean"
  version = "1.0.0"
  name    = "web-1"
}

module "droplet" {
  source  = "robertdebock/droplet/digitalocean"
  version = "1.0.0"
  name    = "web-2"
}
```

The benefit of using a module is that you can fix mistakes just once, (in the module) and you do not need to change your Terraform code that uses the module.

As you can see the `version = 1.0.0` is used. [Versioning](https://semver.org/) is important, you can indicate a few things:

1. The MAJOR version (`1`) indicates the compatibility. `2.0.0` is not compatible with `1.0.0`.
2. The MINOR version (`0`) indicates the features. If this number increases, a new feature should be available.
3. The PATH version (`0`) indicates the bugfixes. If this number increases, a problem has been fixed.

Number can go beyond `9`, so a version a `3.2.13` is possible.

Many vendors do not use [SemVer](https://semver.org/), rather use a new version for marketing purposes.

Learn how to write Terraform modules:

[HashiCorp teaches](https://learn.hashicorp.com/collections/terraform/modules) [Terraform modules](https://learn.hashicorp.com/tutorials/terraform/module-create?in=terraform/modules).

The [documentation](https://www.terraform.io/docs/modules/index.html) may also help.

## Best practices

1. Use [published modules](https://registry.terraform.io/browse/modules) when possible
2. Make modules as small as possible.
3. Use sane defaults. (for example `region` and `size`.)
4. Use no configuration in modules. (It should be usable by anybody.)
5. Use explicit variable names. (Not `r` but `region` for example.)
6. Create a `README.md` explaining the features.
7. Add a `LICENSE` before publishing.
8. Put `terraform.tfstate`, `terraform.tfstate.backup`, `.terraform` and `*.tfvars` in [`.gitignore`](https://github.com/github/gitignore/blob/master/Terraform.gitignore).
9. 

# Questions:

1. Why would you write a module?
2. Where can you find and download modules?
3. By looking at the downloads, what is the most used provider? (AWS, Azure or GCP)
