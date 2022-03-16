# Introduction.

|expected time|requirements|
|-------------|------------|
|45 minutes   |none        |

Goal: Get to know each other and hear about how the course will be held.

## Assignment

Please tell something about yourself.

- [ ] Who are you?
- [ ] From 0 to 10, what's your experience with: git, cloud, infrastructure as code, terraform?
- [ ] What do you want to learn?

## Howto

We need to setup the environment where we are going to play on.

## Where?

On the [lab instances](https://github.com/robertdebock/terraform-playground) all [tools](https://github.com/robertdebock/terraform-playground/blob/master/cloud-init.yml) are installed. You don't have to use these machines, you can also use your laptop or some shared server.

### Let's authenticate (GCP)

This depends a bit per environment. Generic steps are described [here](https://registry.terraform.io/providers/hashicorp/google/latest/docs/guides/getting_started).

The general requirements are:
- You need an account to [login](https://registry.terraform.io/providers/hashicorp/google/latest/docs/guides/getting_started): `gcloud auth application-default login`
- You need to [create a project](https://cloud.google.com/sdk/gcloud/reference/projects/create) to try exercises in. (You'll probably throw this project away when the course is done.)

### Let's authenticate (Azure)

For most users:

```shell
az login
```

You can add `--use-device-code` to authenticate using Microsoft Authenticator.

To use a specific subscription, issue:

```shell
az account set --subscription x-y-z-a-b
```

### Let's get some code

In the [BASIC](../BASIC) course, people have built:

- [This Azure code](https://github.com/hashicorp/learn-terraform-azure).
- [This GCP code](https://github.com/robertdebock/terraform-gcp-firewall/blob/master/instance.tf).

Please `git clone` it to your workspace, we'll start with that.

## Explanation

- Please ask questions when you have them.
- Please keep your camera on most of the time.
- If you run into issues, please share your screen to troubleshoot together.
- A typical chapter has an explanation, exercises and a summary.
- You can take a break whenever you need to.
