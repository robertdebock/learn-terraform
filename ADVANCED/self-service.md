# Self Service

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|30 minutes   |A computer with Terraform installed, terraform knowledge.|

Goal: Get an understanding how to apply Terraform in a scalable way.

## Explanation

This topic depends heavily on your organization.

### Small organization

If you can name your servers (and remember most names), you can have one department manage the whole infrastructure. In this case, self-service is hardly applicable. A person/group that needs resources simply walks to the infrastructure deparment and requests machines.

Terraform can be installed on a shared server, even remote state and/or locking is not very important.

### Medium organization

When an organization grows, there comes a point where one department has troubles managing the whole infrastructure. Locking starts to become an issue, remote state becomes important. There are however specialists that understand the "whole infrastructure".

One group managing all (Terraform) infrastructure starts to become a bottle-neck. Requests are piling up and delivery times start to slip. Basically nobody is impressed by infrastructure as code or Terraform.

### Large organization

At some point it becomes impossible for one person or one group of people to manage the whole infrastructure.

In this scenario it's time to give the hundreds of team a way to describe their own infrastructure. This is in line with the Dev Ops way of thinking; less handovers, end-to-end responsibility. All members of a team can contribute to all aspects of a product or service.

Here multiple groups get to use Terraform. Each team has a limited view of the infrastructure; just the resources required for their product or service.

Remote state, [Terraform Cloud](https://app.terraform.io/) or [Terraform Enterprise](https://www.terraform.io/docs/enterprise/index.html) become required.

[Terraform Cloud](https://app.terraform.io/) is free to use and has many features that [Terraform Enterprise](https://www.terraform.io/docs/enterprise/index.html) offers.

[Terraform Enterprise](https://www.terraform.io/docs/enterprise/index.html) offers these capabilities.
- Private module registry.
- Use [Sentinel](https://docs.hashicorp.com/sentinel/concepts/policy-as-code) for policy as code.
- More team managment and workspace capabilities.
- Role based access control.
- Price prediction.
- Auditable.
- Support

## Demo

Let's go to [Terraform Cloud](https://app.terraform.io/) and walk through the setup of a workspace connected to a repository.

1. Open [Terraform Cloud](https://app.terraform.io/).
2. Select `New workspace`.
3. Select `Version control workflow`.
4. Choose `GitHub`.
5. Enter `robertdebock/terraform-demo` in the bottom.
6. Under `Advanced options` set the branch to `cloud`.
7. Click `Create workspace`.
8. Click `Configure variables`.
9. Add a Terraform Variable called `do_token`. (Select `Sensitive`).

You can now manually queue a plan.

## Assignment

- [ ] Discuss what a good way of doing self-service is with each other.

## Questions

1. Is your organization "small", "medium" or "large"?
2. Do you have self-service capabilities in place?

## Solution
