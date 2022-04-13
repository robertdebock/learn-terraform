# Store state on GCP

| expected time | requirements                                             |
|---------------|----------------------------------------------------------|
| 45 minutes    | A computer with Sentinel installed, terraform knowledge. |

Goal: See how remote state on GCP works.

## Explanation

So far you have been using a "local state", basically just some files in your repository. This does not allow collaboration, the state is only on your laptop.

There are multiple reasons to use remote state:

1. Collaborate; others can use the state too.
2. Local state files can be lost.
3. Remote state can have access permissions.

This example looks at Google mostly, but there are many more place where you can store remote state:

1. Terraform Enterprise.
2. Terraform Cloud.
3. AWS S3.
4. Azure Storage.
5. Many more.

Do not confuse the data object [remote state](https://www.terraform.io/language/state/remote-state-data) with remote state. (Although it's interesting!)

## Demo

See [this](https://github.com/robertdebock/terraform-gcp-backend) repo.

## Assignment

In this assignment we are going to [migrate](https://www.terraform.io/cli/commands/init#backend-initialization) the local state to GCP.

1. Pick any of the repositories you have already created.
2. Run `terraform apply` to create the resources. State will be local.

You are now ready to migrage state.

1. Make a bucket. (Either manually, or using Terraform.)
2. Add or edit `terraform.tf` and set the `backend` to `gcs`.
3. Set the correct `bucket`.
4. Optionally set the `prefix`.
5. Run `terraform init -migrate-state`.

When you've answered 'yes', your state is remote. We're going to migrate back to a local state file.

1. Comment all lines in, or remove `terraform.tf`.
2. Run `terraform init -migrate-state`.

When you've answerd 'yes', your state is now local again.

## Questions:

1. Are you using, or would you consider to use remote state?
2. What are some disadvanteges of remote state?

## Sources

- [HashiCorp on remote state](https://www.terraform.io/language/state/remote).
