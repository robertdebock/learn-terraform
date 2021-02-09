# Using GIT for version control.

|expected time|requirements|
|-------------|------------|
|60 minutes   |a browser   |

Goal: Learn to work with Git.

## Explanation

You can write code on your laptop or a shared (bastion/jump) server. Without a [version control system](https://en.wikipedia.org/wiki/Version_control) system, it's difficult to work together, track changes, understand who has done what and many other issues.

Using a version control system is sort of required when writing code.

"If it's not in git, svn or cvs, it does not exist."

## Introduction

Git is a [version control system](https://en.wikipedia.org/wiki/Version_control). Alternatives are:

- svn
- cvs

## Howto

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

## Demo

## Assignment

- [ ] Let's [learn Git](https://www.katacoda.com/courses/git)

## Bonus assignment

- [ ] Correct this tyyypo by making an [merge reqeust](https://github.com/robertdebock/learn-terraform/edit/master/BASIC/using-git-for-version-control.md)

You're done when you can use these commands: (Likely scenario 1, 2 and 3.)

- `git clone`
- `git add`
- `git commit`
- `git push`
- `git pull`

[An explanation on Git](https://www.youtube.com/watch?v=Y9XZQO1n_7c) if you've got time to spare.

## Questions

1. What is the difference between `git` and [GitHub](https://github.com/) or [GitLab](https://gitlab.com/)?
2. Can you explain what `git fetch`, `git merge`, `git pull` do?
3. `git` and CI/CD are commonly used together, do you know the differences?
