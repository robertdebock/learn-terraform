# Learn Terraform

## Introduction (30 min.) 

- Who are you?
- From 0 to 10, what's your experience with: linux, cloud, git, terraform?
- What do you want to learn?

[HashiCorp on Terraform](https://www.terraform.io/):

> Terraform is an open-source infrastructure as code software tool that provides a consistent CLI workflow to manage hundreds of cloud services. Terraform codifies cloud APIs into declarative configuration files

Let's break that down:

- Open-source: You can view the [code](https://github.com/hashicorp/terraform). There is an [enterprise](https://www.terraform.io/docs/enterprise/index.html) and [cloud offering](https://www.terraform.io/docs/cloud/index.html) too.
- Infrastructure as code: You can describe in [plain text](https://github.com/robertdebock/terraform-demo/blob/master/do.tf) what infrastructure you need.
- CLI workflow: From a Linux machines, you can use the `terraform` binary.
- Cloud services: Terraform describes "resources", which can be: machines, ip-addresses, loadbalancers, etc.
- declarative configuration: You describe the infrastructure, Terraform will build (or destroy) it.

## Introduction to Infrastructure as Code with Terraform (30 min.) 

### Why Infrastructure as Code (IaC)?

- Code is repeatable.
- It's easy to work together.
- Faster. (After you've learned the tools)
- Code can have a version.
- Modules can be tested.
- Easy to test on a non-production environment.
- Easy to learn by reading, less documentation.

[Benefits are listed here](https://phoenixnap.com/blog/infrastructure-as-code-best-practices-tools)

### Terraform

Let's learn a bit more on Terraform:

- [This video by IBM](https://www.youtube.com/watch?v=HmxkYNv1ksg) (08:43).
- [This video from HashiCorp](https://www.youtube.com/watch?v=h970ZBgKINg) (18:38).

There are many [providers](https://registry.terraform.io/browse/providers) and [modules](https://registry.terraform.io/browse/modules).

Terraform keeps [state](https://www.terraform.io/docs/state/index.html). This means it can compare the (local) state to the desired state, making deployment faster. This also allows people or teams to collaborate.

```text
+----- Team A ------+   +----- Team B ------+
| resources.tf      |   | resources.tf      |
| terraform.tfstate |   | terraform.tfstate |
+-------------------+   +-------------------+
         |                       |
         V                       V
+------------- Cloud provider X --------------+
| +--- instance A ---+   +--- instance B ---+ |
| |                  |   |                  | |
| +------------------+   +------------------+ |
+---------------------------------------------+
```

Having state means Terraform will remove resources that are not described anymore. Here you see two code snippets, if you were to `terraform apply moment-0.tf` first, followed by `terraform apply moment-1.tf`, the `digitalocean_droplet` with the name `web-1` would be removed.

#### moment-0.tf

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

#### moment-1.tf

```
resource "digitalocean_ssh_key" "example" {
  name       = "example"
  public_key = file("id_rsa.pub")
}
```

This differs from for example Ansible, that only ensures described resources exists, but will not remove resources if they are removed from the code (stolen from the [Ansible docs](https://docs.ansible.com/ansible/latest/collections/community/digitalocean/digital_ocean_module.html):

#### moment-0.yml

```yaml
- name: ensure an ssh key is present
  community.digitalocean.digital_ocean:
    state: present
    command: ssh
    name: example
    ssh_pub_key: 'ssh-rsa AAAA...'

- name: create a new droplet
  community.digitalocean.digital_ocean:
    state: present
    command: droplet
    name: web-1
    size_id: 1gb
    region_id: ams3
    image_id: fedora-32-x64
```

#### moment-1.tml

```yaml
- name: ensure an ssh key is present
  community.digitalocean.digital_ocean:
    state: present
    command: ssh
    name: example
    ssh_pub_key: 'ssh-rsa AAAA...'
```

If you would apply `moment-0.yml` followed by `moment-1.tml`, the droplet `web-1` would **NOT** be removed.

## Using GIT for version control. (60 min.) 

### Introduction

Git is a [version control system](https://en.wikipedia.org/wiki/Version_control). Alternatives are:

- svn
- csv

Let's [learn Git](https://www.katacoda.com/courses/git)

## Build Infrastructure, incl. syntax explanation.(120 min.)

## Change Infrastructure (30 min.) 

## Destroy Infrastructure (30 min.) 

## Define Input Variables (60 min.) 

## Query Data with Output Variables (60 min.) 

## Store Remote State (60 min.) 

## Writing modules (120 min.) 

## CI/CD concepts (30 min.)

## Use-cases (bonus) (120 min.)
