# Testing experiment

| expected time | requirements                                              |
|---------------|-----------------------------------------------------------|
| 30 minutes    | A computer with Terraform installed, terraform knowledge. |

Goal: Try the new "testing" experiment.

## Explanation

Terraform spins up resources, you can test if that works in CI. But, by testing `terraform apply`, you basically test if Terraform was able to spin up the resources, not if whatever you spun up actually works.

Functional testing could include some of these cases:

- Is a TCP port available?
- Does the web-page return a 200 status?
- Does the web-page return some pattern on the body?

There are probably many more cases you may describe.

## Howto

WARNING: Here be dragons, the testing **experiment** is not very stable or intuitive.

An extra directory must be created: `tests`. In there a directory `default` must be created. (See "limitation-1")

In that directory (`tests/default/`) you can add any `.tf` file to describe the tests.

Because this is an experiment, you need to explicitly enable the "provider".

```hcl
terraform {
  required_providers {
    test = {
      source = "terraform.io/builtin/test"
    }
  }
}
```

The module must be called, even if it's a root-module. (root-module is not a module.)

```hcl
# The module must be called `main`.
module "main" {
  source = "../.."
  # Variables are not passed from here to the use module.
  text   = "Will not be passed to the used module!"
}
```

Variables can't be passed as you may expect. (See "limitation-2".)


Now you can start testing by using the `test_assertions` resource.

```
resource "test_assertions" "my_local_file" {
  component = "my_file_checks"

  check "my_check_if_file_exists" {
    description = "The file exists."
    condition   = fileexists("foo.bar")
  }

  check "my_check_if_file_contains_pattern" {
    description = "The file contains a specific pattern"
    condition   = file("foo.bar") == "Hello world!"
  }
}
```

In the example above, the two tests basically have a dependency:

- If `my_check_if_file_exists` fails, don't even try `my_check_if_file_contains_pattern`.

One can argue that all test must always run, so no dependency exists.

## Demo

A [generic example](https://github.com/robertdebock/terraform-testing).

The order differs from the documentation; `terraform test` should `apply`, but it does not. See "limitation-3".

## Assignment

- Expand the [example code](https://github.com/robertdebock/terraform-testing) to test that the pattern "Not in here" is not found in the file.

In case your code fails, the resources are destroyed. Would have been nice to inspect the (faulty) resources before they are cleaned up. See "limitation-4". On top of that `output` or `resource "local_file"` (To drop a file with some data) are not allowed or working. See "limitation-5".

## Limitations

- limitation-1: Why must the folder be called `default`?
- limitation-2: Variables can't be passed from `tests/default/*.tf`. So, the values will come from the called module. If the module has mandatory variables, these must be set using some other method.
- limitation-3: The command `terraform test` should `apply`, `test` and `destroy`, but the `apply` does not happen automatically. You may need: `terraform apply --auto-approve && terraform test`.
- limitation-4: Failed tests destroy resources. This makes it difficult to troubleshoot "broken" or "incorrect" resources.
- limitation-5: You can't use regular `output` or random `resources` in the `tests/default/*.tf`. This would have been nice to troubleshoot.
