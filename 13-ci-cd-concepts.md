# CI/CD Concepts

|expected time|requirements              |
|-------------|--------------------------|
|60 minutes   |Basic terraform knowledge.|

Now that you are familiar with Terraform, you can automate deployments.

## Modules

```text

\O/      +--- GitHub|GitLab ---+
 |  ---> | - module            |
/ \      +---------------------+
```

Best practices for modules:

1. Use one repository per module.
2. Use `terraform validate`.
3. Use `terraform fmt`.
4. Use [tflint](https://github.com/wata727/tflint).
5. Release version upon succesful tests.
6. Use [Semantic Versioning 2.0.0](https://semver.org/) versioning.

## Repository

A typical repository uses either providers directly or modules. The repository contains all information required to build the infrastructure. (Except sensitive values such as usernames and password.)

By applying (`terraform apply`) the Terraform code, your environment will be modified. If you setup CI/CD, you have the benefit of automatic changes, but the drawback of unexpected (automatic) changes happening to your environment.

Here is an example for BitBucket:

```yaml
image: hashicorp/terraform:full
pipelines:
    default:
        - step:
            script:
                - terraform init
                - terraform validate
                - terraform plan
    branches:
        master:
            - step:
                script:
                    - terraform init
                    - terraform validate
                    - terraform plan -out "planfile"
                    - terraform apply -input=false -auto-approve "planfile"
```

Here is an example that can be used for GitLab:

```yaml
image:
  name: hashicorp/terraform:0.13.5
  entrypoint:
    - '/usr/bin/env'
    - 'PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin'

before_script:
  - rm -rf .terraform
  - terraform --version
  - terraform init

stages:
  - validate
  - plan
  - apply

validate:
  stage: validate
  script:
    - terraform validate

plan:
  stage: plan
  script:
    - terraform plan -out "planfile"
  dependencies:
    - validate
  artifacts:
    paths:
      - planfile

apply:
  stage: apply
  script:
    - terraform apply -input=false -auto-approve "planfile"
  retry: 2
  dependencies:
    - plan
  when: manual
  only:
    refs:
      - master
```
