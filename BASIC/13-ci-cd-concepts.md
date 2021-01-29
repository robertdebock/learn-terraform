# CI/CD Concepts

|expected time|requirements              |
|-------------|--------------------------|
|60 minutes   |Basic Terraform knowledge.|

Now that you are familiar with Terraform, you can automate deployments.

## What?

Continuous Integration/Continouos Development (CI/CD) is the practice of testing frequently and pushing changes to production frequently. The idea is that small changes can be tested and integrated (into production) quickly and safely.

CI/CD helps with these aspects:

1. Catch mistakes as early as possible.
2. Tests prove that changes work (or fail).
3. It's easy to bring changed to production.

(And likely many other benefits.)

How you setup CI/CD depends a bit on the facilities you have, but generally speaking all version control systems (GitHub/GitLab/BitBucket/Jenkins/Travis) have some kind of `pipeline`-mechanism. Such a mechanism wakes up when a push (with commits) is done to a repository.

With Terraform you'll probably have two types of repositories:

1. Terraform Modules
2. Terraform integrations

The Terraform Modules are independent, small re-usable pieces. Tests should happen on these repositories frequently.
The Terraform integrations use modules to describe an infrastructure of a product or service. Tests on these repositories can happen and eventually the integration can be `apply`-ed to the production environment. This is typically a manual step.

CI/CD typically uses three stages:

1. Build - You could see this as `terraform apply`.
2. Test - Is the module or integration doing what it should?
3. Release - Works? Release a new version.

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

## Integration

```text

\O/      +--- GitHub|GitLab ---+
 |  ---> | main.tf             |
/ \      | versions.tf         | <- Terraform Registry
         +---------------------+
```

A typical repository uses either providers directly or modules. The repository contains all information required to build the infrastructure. (Except sensitive values such as usernames and password.)

By applying (`terraform apply`) the Terraform code, your environment will be modified. If you setup CI/CD, you have the benefit of automatic changes, but the drawback of unexpected (automatic) changes happening to your environment.

Here is an example for BitBucket:

```yaml
---
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
        trigger: manual
        script:
          - terraform init
          - terraform validate
          - terraform plan -out "planfile"
          - terraform apply -input=false -auto-approve "planfile"
```

Here is an example that can be used for GitLab:

```yaml
---
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
