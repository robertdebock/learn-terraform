# `try`

| expected time | requirements                                              |
|---------------|-----------------------------------------------------------|
| 30 minutes    | A computer with Terraform installed, terraform knowledge. |

Goal: Write modules that have optional parameters.

## Explanation

Sometimes you want to use a module that has many parameters, some are optional. For example;

```hcl
repositories = {
  my_repo_5 = {
    description = "My wonderful fifth repository."
  },
  my_repo_6 = {
    description  = "My wonderful sixth repository."
    homepage_url = "https://robertdebock.nl/"
    has_issues   = false
    has_projects = false
    has_wiki     = false
  }
}
```

The example above shows a map of two entries; `my_repo_5` and `my_repo_6`. The `my_repo_6` has more options than `my_repo_5`. This means the module should `try` to see if a variable is set, otherwise return `null`.

`null` means the whole parameter is removed, as if it was not described.

## Demo

See [here](https://github.com/robertdebock/terraform-try).

## Howto

Here is how to `try` parameters:

```hcl
module "github" {
  source   = "../../"
  for_each = var.repositories

  repository_name         = each.key
  repository_description  = each.value.description
  repository_homepage_url = try(each.value.homepage_url, null)
  repository_has_issues   = try(each.value.has_issues, null)
  repository_has_projects = try(each.value.has_projects, null)
  repository_has_wiki     = try(each.value.has_wiki, null)
}
```

## Solution

See [this repository](https://github.com/robertdebock/terraform-github-deployment/blob/master/examples/repositories/main.tf).
Or [more complex](https://github.com/robertdebock/terraform-aws-vault).

## Sources

- [try](https://www.terraform.io/docs/language/functions/try.html)
