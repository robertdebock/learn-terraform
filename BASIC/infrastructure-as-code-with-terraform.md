# Introduction to Infrastructure as Code with Terraform

|expected time|requirements|
|-------------|------------|
|60 minutes   |none        |

Goal: Understand what Infrastructure as code is.

## Why Infrastructure as Code (IaC)?

What is the problem IaC is trying to solve?

1. Manual work is difficult.
2. Manual work is error prone.
3. Manual work is slow.
4. Manual work leads to "pets" over "cattle".

Not specifically Terraform, but IaC (Infrastructure as Code) in general has these benefits:

- Code is repeatable.
- It's easy to work together.
- Faster. (After you've learned the tools)
- Code can have a version.
- Code is auditable.
- Modules (or units) can be tested.
- Easy to test on a non-production environment.
- Easy to learn by reading, less documentation.

[Benefits are listed here](https://phoenixnap.com/blog/infrastructure-as-code-best-practices-tools)

There are some drawback too:

- Higher abstraction level/harder. We'll try to address that here!
- Hard to combine with manual work.
- Requires tooling. (Terraform, GitLab/GitHub/BitBucket)

## Terraform

Let's learn a bit more on Terraform:

- Terraform about IaC. [AWS](https://learn.hashicorp.com/tutorials/terraform/infrastructure-as-code?in=terraform/aws-get-started), [Azure](https://learn.hashicorp.com/tutorials/terraform/infrastructure-as-code?in=terraform/azure-get-started), [GCP](https://learn.hashicorp.com/tutorials/terraform/infrastructure-as-code?in=terraform/gcp-get-started)
- [This video by IBM](https://www.youtube.com/watch?v=HmxkYNv1ksg) (08:43).
- [This video from HashiCorp](https://www.youtube.com/watch?v=h970ZBgKINg) (18:38).

There are many [providers](https://registry.terraform.io/browse/providers) and [modules](https://registry.terraform.io/browse/modules).

Terraform keeps [state](https://www.terraform.io/docs/state/index.html). State is sort of a book-keeping of what Terraform has created. This means it can compare the (local) state to the desired state, making deployment faster and allowing users to clean-up resources remove from the configuration. This also allows people or teams to collaborate.

```text
+----- Team A ------+     +----- Team B ------+
| resources.tf      |     | resources.tf      |
| terraform.tfstate |     | terraform.tfstate |
+-------------------+     +-------------------+
         |                         |
         V                         V
+------------- Cloud provider X --------------+
| +--- instance A ---+   +--- instance B ---+ |
| |                  |   |                  | |
| +------------------+   +------------------+ |
+---------------------------------------------+
```

Having state means Terraform will remove resources that are not described anymore.

## Demo

Actually; let's create [your machines](https://github.com/robertdebock/terraform-playground).

- Username: username
- Password: password

You are free to use this machine. If you'd like to run Terraform from another machine, maybe your laptop, please [install Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli).

## Questions

1. Terraform keeps state, what is the benefit?
2. Terraform and configuration management differ, for what situation would you use either?
3. In your own words, what are some benefits of infrastructure as code?
4. You (maybe) have see it can take a while for the "playground" machines to be ready. What could you do to make this deployment quicker?

## What tools to use when?

There is no clear answer to this question. I suggest to use the right tool for the type of work. Most companies use Terraform and some other configuration management system, for example.

- Terraform to manage infrastructure.
- Ansible, Puppet, Chef or SaltStack for the configuration of the instances.

In other words, just Terraform is not always sufficient.
