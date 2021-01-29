# CI/CD for modules

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|60 minutes   |A computer with Terraform installed, terraform knowledge.|

Setup CI/CD for Terraform modules.

## Explanation

Testing helps you to keep your modules in a good state and makes it easier to contribute.

- [ ] A discussion before we begin: "What can we test of a Terraform module?" ([Possible-answers](2-cicd-for-modules-test.md))

## Howto

Let's take an example BitBucket CI/CD file. (It's not compelete, you'll make it complate later.)

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

## Assignment

- [ ] For your version control system, write a CI/CD file that tests a module. The tests may be simple, they can be extended later.

This may take some time, but it's well worth the effort as these pipelines will run quite frequently. We'll compare eachothers code later to learn from each other.

With CI/CD, always start with the smallest unit/component. This ensures you can deliver value incrementally instead of a "waterfall" approach.

## Bonus assignment

- [ ] For a module you use/maintain, add [input validation](https://www.terraform.io/docs/language/values/variables.html#custom-validation-rules) to test if the input given was correct. Here is a [hint](2-cicd-for-modules-input-validation.md)
- [ ] Once you have input validation, change the pipeline so it tests failing input. (So the input should be incorrect, maybe a `string` where `number` is only allowed, and the pipeline should successfully test the failure.)

## Questions

1. Would you `terraform apply` the code in CI when testing a module?
2. If you would `terraform apply`, how would you make sure `terraform destroy` runs whatever the output of `terraform apply`. ([hint](https://bitbucket.org/blog/after-scripts-now-available-for-bitbucket-pipelines)).

## Solution

- A [GitLab](2-cicd-for-modules-gitlab.yml)
- A [GitHub Action](https://github.com/robertdebock/terraform-action).
