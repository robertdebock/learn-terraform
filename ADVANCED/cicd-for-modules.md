# CI/CD for modules

|expected time|requirements                                               |
|-------------|-----------------------------------------------------------|
| 75 minutes  | A computer with Terraform installed, terraform knowledge. |

Goal: Setup CI/CD for Terraform modules.

## Explanation

Testing helps you to keep your modules in a good state and makes it easier to contribute.

- [ ] A discussion before we begin: "What can we test of a Terraform module?" ([Possible-answers](cicd-for-modules-test.md))

## Howto

### BitBucket

Let's take an example BitBucket CI/CD file. (It's not complete, you'll make it complete later.)

Add a file to the repository containing a Terraform module called `bitbucket-pipelines.yml`:

```yaml
---
image: hashicorp/terraform:full

pipelines:
  default:
    - step:
      script:
        - terraform init
```

And a [GitHub actions example](https://github.com/robertdebock/terraform-aws-cluster/blob/master/.github/workflows/terraform.yml). Be aware the the different scenarios (directories in `examples` need to be listed in the action.

### GitHub

There are [many actions](https://github.com/marketplace?query=terraform&type=actions) that you can use. Pick one that suits your situation.

A realistic example can be found [here](https://github.com/robertdebock/terraform-aws-vault/blob/master/.github/workflows/terraform.yml).

## Assignment

- [ ] For your version control system, write a CI/CD file that tests a module. The tests may be simple, they can be extended later.

This may take some time, but it's well worth the effort as these pipelines will run quite frequently. We'll compare each others code later to learn from each other.

With CI/CD, always start with the smallest unit/component. This ensures you can deliver value incrementally instead of a "waterfall" approach.

## Bonus assignments

- [ ] For a module you use/maintain, add [input validation](https://www.terraform.io/docs/language/values/variables.html#custom-validation-rules) to test if the input given was correct. Here is a [hint](cicd-for-modules-input-validation.md)
- [ ] Once you have input validation, change the pipeline so it tests failing input. (So the input should be **incorrect**, maybe a `string` where `number` is only allowed, and the pipeline should successfully test the failure.) To reverse the exit-status of a command, use `!`, for example `! false` returns an exit-code of `0`.
- [ ] If time permits; configure secrets that allow `terraform apply` and `terraform destroy`.

## Questions

1. Would you `terraform apply` the code in CI when testing a module?
2. If you would `terraform apply`, how would you make sure `terraform destroy` runs whatever the output of `terraform apply`. ([hint](https://bitbucket.org/blog/after-scripts-now-available-for-bitbucket-pipelines)).

## Hints

You may need to place these "secret variables" to the CI system:

- `AZURE_AD_CLIENT_ID`
- `AZURE_AD_CLIENT_SECRET`
- `AZURE_AD_TENANT_ID`
- `AZURE_SUBSCRIPTION_ID`

For GitLab users, a [template](https://docs.gitlab.com/ee/user/infrastructure/#quick-start) can be used.

## Solution

- A [GitLab](cicd-for-modules-gitlab.yml)
- A [GitHub Action](https://github.com/robertdebock/terraform-action).
