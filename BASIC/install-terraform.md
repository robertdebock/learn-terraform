# Install terraform

|expected time|requirements|
|-------------|------------|
|60 minutes   |a computer  |

Goal: Have terraform installed.

## Explanation

Terraform is a program that needs to be installed. It's quite simple, but required.

The Terraform CLI is a simple binary, no services/servers/daemon, no specific users, etc.

## Howto

This depends a bit on the environment you're working in.

- There are repositories for Linux (`apt`, `dnf` and `yum`).
- You can [download the binary](https://releases.hashicorp.com/terraform/).
- To manage Azure infrastructure, you also need [azure-cli](https://pypi.org/project/azure-cli/). Follow [this guide](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=azure-cli) for Windows computers.

Have a look at [this playground repository](https://github.com/robertdebock/terraform-playground) that can be used to spin up machine to try terraform on.

## Demo

## Assignment

You first need to install terraform. Identical for all providers:

- [AWS](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/aws-get-started)
- [Azure](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/azure-get-started)
- [GCP](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/gcp-get-started).

To verify that you are done, please enter this command:

```shell
terraform --version
```

## Questions

1. What installation method would you prefer?
2. How was terraform installed? (If it was installed for you.)
