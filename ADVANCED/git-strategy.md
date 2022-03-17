# Git strategy

| expected time | requirements |
|---------------|--------------|
| 30 minutes    | Not a lot.   |

Goal: Discuss the different git strategies.

## Explanation

There are many ways to work with Git. Let's discuss a few.

### One branch

This strategy tries to get all development back to a single branch, say `main` or `master`. There can be extra branches that hold active development efforts, but the intent is to bring those changes back to the default branch.

On succesful integration into the default branch, a new version is released. This basically means the released version is expected to work.

```text
                              +--- version: 1.2.3
                             /
----+------ (master) -------+----
     \                     /
      +--- (my_branch) ---+
```

#### Benefits

- This is quite a simple strategy.
- Dead branches can be removed.
- The version indicates a usable state of the code.

#### Drawbacks

- No variations possible.

### Multiple branches

This strategy requires a bit more maintenance; there will be multiple branches, maybe an environment will use a specific branch.

```text
---+--- (development) ---
    \
     +--- (test) ---
      \
       +--- (acceptance) ---
        \
         +--- (production) ---
```

In this strategy, experiments happen in `development`. Once working, a merge can be done to `test`. When that's working, a merge can be done to `acceptance` and so on.

This means `production` is last in line.

There can be (and likely are) multiple branches before `development`.

#### Benefits

- There can be various versions (branches) in use.
- Easy to "review" before pushing (with a "pull request" (GitHub) or "merge request" (GitLab)) to production.

#### Drawbacks

- There are no "stable" versions.
- This strategy may be overwhelming and required good branch-managment.
- A merge mistake can skip a branch. (`development` to `production` for example.)

## Assignment

- [ ] Review the [terraform network](https://github.com/hashicorp/terraform/network). What strategy is used here?

## Questions:

1. For yourself/colleagues/company, what is the best strategy?
