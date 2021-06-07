# `count` or `for_each`?

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|30 minutes   |A computer with Terraform installed, terraform knowledge.|

Goal: Understand when to use `count` and when `for_each`.

## Explanation

Most programming languages have some way to `loop`. An example in `bash`:

```shell
for item in a b c ; do
  echo "${item}"
done
```

Will show:

```text
a
b
c
```

Typically you write a loop to [prevent repetition](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself). It makes code shorter and more readable, plus mistakes are also not repeated.

|parameter        |count      |for_each|
|-----------------|-----------|--------|
|terraform version|very early |1.12.6  |
|input            |map or list|number  |
|situation        |multiple **similar** resources|multiple **related** resources|

## Howto

### `count` example

```hcl
resource "azurerm_resource_group" "example" {
  count    = 3
  name     = "example-${count.index}"
  location = "West Europe"
}
```

In the example above, 3 resources are created, the only variable you can use is a number, stored under `count.index`.

### `for_each` example

There are two ways to use `for_each`:

#### Using a list of strings

This is the simples form; you simply pass a list of strings (actually a set) and you can reuse that one of the strings from the list in your Terraform codel.

```hcl
resource "azurerm_resource_group" "example" {
  for_each = toset( ["westeurope", "easteurope"] )
  name     = "my_rg"
  location = each.value
}
```

#### Using a map

Here you can pass both a `key` and `value` for that key to your Terraform code.

```hcl
resource "azurerm_resource_group" "example" {
  for_each = {
    my_rg_one = "westeurope"
    my_rd_two = "easteurope"
  }
  name     = each.key
  location = each.value
}
```

In the example above, both the `key` (left from `=`) and the `value` (right from `=` are used.)

This is a little more complex, so use it with caution; newcomers to Terraform may be confused.

## Assignment

- [ ] Rewrite [example 1](count_or_for_each_assignments.md#example-1) to use `count.`
- [ ] Rewrite [example 2](count_or_for_each_assignments.md#example-2) to use `for_each` with a list.
- [ ] Rewrite [example 3](count_or_for_each_assignments.md#example-3) to use `for_each` with a map.

## Questions

1. In the example of `count` (scroll up a little), what are the names of resource groups that will be created?
2. Can you think of (or even better: show) code that can be impoved using `count` or `for_each`?

## Solution

- [Example 1](count_or_for_each_solutions#example-1)
- [Example 2](count_or_for_each_solutions#example-2)
- [Example 3](count_or_for_each_solutions#example-3)

## Sources

- [count](https://www.terraform.io/docs/language/meta-arguments/count.html)
- [for_each](https://www.terraform.io/docs/language/meta-arguments/for_each.html)
- [Medium](https://medium.com/@business_99069/terraform-count-vs-for-each-b7ada2c0b186)
