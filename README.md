# Learn Terraform

## Introduction (30 min.) 

[HashiCorp on Terraform](https://www.terraform.io/):

> Terraform is an open-source infrastructure as code software tool that provides a consistent CLI workflow to manage hundreds of cloud services. Terraform codifies cloud APIs into declarative configuration files

Let's break that down:

- Open-source: You can view the [code](https://github.com/hashicorp/terraform). There is an [enterprise](https://www.terraform.io/docs/enterprise/index.html) and [cloud offering](https://www.terraform.io/docs/cloud/index.html) too.
- Infrastructure as code: You can describe in [plain text](https://github.com/robertdebock/terraform-demo/blob/master/do.tf) what infrastructure you need.
- CLI workflow: From a Linux machines, you can use the `terraform` binary.
- Cloud services: Terraform describes "resources", which can be: machines, ip-addresses, loadbalancers, etc.
- declarative configuration: You describe the infrastructure, Terraform will build (or destroy) it.

[This video by IBM](https://www.youtube.com/watch?v=HmxkYNv1ksg) explains Terraform, just as [this video from HashiCorp](https://www.youtube.com/watch?v=h970ZBgKINg) .

## Introduction to Infrastructure as Code with Terraform (30 min.) 

## Why Infrastructure as Code (IaC)?

- Code is repeatable.
- It's easy to work together.
- Faster. (After you've learned the tools)
- Code can have a version.
- Modules can be tested.
- Easy to test on a non-production environment.
- Easy to learn by reading, less documentation.

[Benefits are listed here](https://phoenixnap.com/blog/infrastructure-as-code-best-practices-tools)

## Using GIT for version control. (60 min.) 

## Build Infrastructure, incl. syntax explanation.(120 min.)

## Change Infrastructure (30 min.) 

## Destroy Infrastructure (30 min.) 

## Define Input Variables (60 min.) 

## Query Data with Output Variables (60 min.) 

## Store Remote State (60 min.) 

## Writing modules (120 min.) 

## CI/CD concepts (30 min.)

## Use-cases (bonus) (120 min.)
