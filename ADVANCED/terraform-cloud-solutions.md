# Assignment examples

## Name some benefits of Terraform Cloud over a local installation.

> Terraform is installed for you, no local installation of terraform required.

> A managed service, updates (also to `terraform`) are done for you.

> Allows you to store (sensitive) variables. Otherwise the variables would be stored in code.

> Allows collaboration for teams.

> State is stored remotely.

> `data` object from [another backend](https://www.terraform.io/docs/language/state/remote-state-data.html#example-usage-remote-backend-) can be consumed.

## Where are variables stored when using Terraform Cloud?

> Either in a file (saved in git) or in Terraform Cloud itself.

## You need to manage resources on an isolated network using Terraform Cloud, what can you use?

> You can use [Terraform Cloud Agents](https://www.terraform.io/docs/cloud/agents/index.html).
