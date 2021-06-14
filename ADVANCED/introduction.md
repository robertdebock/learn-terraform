# Introduction.

|expected time|requirements|
|-------------|------------|
|45 minutes   |none        |

Goal: Get to know each other and hear about how the course will be held.

## Assignment

Please tell something about yourself.

- [ ] Who are you?
- [ ] From 0 to 10, what's your experience with: linux, cloud, git, terraform?
- [ ] What do you want to learn?

## Howto

We need to setup the environment where we are going to play on.

### Let's authenticate

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

In the [BASIC](../BASIC) course, people have built [this code](https://github.com/hashicorp/learn-terraform-azure). Please `git clone` it to your workspace, we'll start with that.

## Explanation

- Please ask questions when you have them.
- Please keep your camera on most of the time.
- If you run into issues, please share your screen to troubleshoot together.
- A typical chapter has an explanation, exercises and a summary.
- You can take a break whenever you need to.
