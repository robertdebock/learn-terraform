# CI/CD for releases

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|30 minutes   |A computer with Terraform installed, terraform knowledge.|

Goal Setup CI/CD for Terraform releases.

## Explanation

When you've used Terraform modules, you can start to integrate different modules into a root-module. The pipeline looks quite similar to the Terraform module pipeline.

## Howto

Start with a `bitbucket-pipelines.yml`:


```yaml
---
image: hashicorp/terraform:full

pipelines:
  default:
    - step:
      script:
        - terraform init
```

In this case, we want to also `plan` and `apply`. BitBucket needs to [pass some secrets](https://support.atlassian.com/bitbucket-cloud/docs/variables-and-secrets/) to Terraform in order to connect to the configured providers.

## Assignment

- [ ] Write a pipline to apply terraform code. Use a manual step after all verification steps (validate, lint, etc) are done.

## Questions

1. What's different to this pipeline compared to the module pipeline?

## Solution

- [GitLab](4-cicd-for-releases-gitlab.yml)
