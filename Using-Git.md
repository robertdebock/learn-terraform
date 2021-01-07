# Using GIT for version control. (60 min.) 

## Introduction

Git is a [version control system](https://en.wikipedia.org/wiki/Version_control). Alternatives are:

- svn
- csv

Let's [learn Git](https://www.katacoda.com/courses/git)

You're done when you can use these commands: (Likely scenario 1, 2 and 3.)

- git clone
- git add
- git commit
- git push
- git pull

To test your knowledge: fix this misteeke by making a pull request:

(`YOURNAME` should be replaced by your name, no spaces, for example: `robertdebock`.)

1. `git clone git@github.com:robertdebock/learn-terraform.git`
2. `cd learn-terraform`
3. `git checkout -b YOURNAME`
4. Edit README.md, change "misteeke" to "mistake".
5. `git add README.md`
6. `git commit -m "Fixed a typo"`
7. `git push -u origin YOURNAME`

More [hints here](https://opensource.com/article/19/7/create-pull-request-github)
