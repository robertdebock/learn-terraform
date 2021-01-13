# Using GIT for version control.

|expected time|requirements|
|-------------|------------|
|60 minutes   |a browser   |

## Introduction

Git is a [version control system](https://en.wikipedia.org/wiki/Version_control). Alternatives are:

- svn
- csv

Let's [learn Git](https://www.katacoda.com/courses/git)

You're done when you can use these commands: (Likely scenario 1, 2 and 3.)

- `git clone`
- `git add`
- `git commit`
- `git push`
- `git pull`

[An explanation on Git](https://www.youtube.com/watch?v=Y9XZQO1n_7c) if you've got time to spare.

## How I use Git daily.

Here is what I do to setup a new repository.

```shell
git init
git add .
git commit -m "Initial commit."
```

When the code is sort of ready, I'll create a repository on GitHub and push the code.

```shell
git remote add origin https://github.com/robertdebock/bla.git
git push -u origin master
```

By now CI/CD tests the code and it's never occurred to me that the code was flawless the first attempt. So, fix the issue, try again.

```shell
git add .
git commit -m "Fix something."
git push
```

Some commands can be combined: `git add .` and `git commit -m "Fix something."` can be combined: `git commit -am "Fix something."`

When contributions happen, I'll merge it online, but have to remember to pull.

```shell
git pull
```

# Questions

1. What is the difference between `git` and [GitHub](https://github.com/)|[GitLab](https://gitlab.com/)?
2. `git` and CI/CD are commonly used together, do you know the differences?
