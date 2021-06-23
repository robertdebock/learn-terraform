# Functions

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|30 minutes   |A computer with Terraform installed, terraform knowledge.|

Goal: Understand what functions are and how to apply (some of) them.

## Explanation

Terraform has many built-in [function](https://www.terraform.io/docs/language/functions/index.html). Some noteworthy:

- [`length`](https://www.terraform.io/docs/language/functions/length.html)
- [`can`](https://www.terraform.io/docs/language/functions/can.html)
- [`file`](https://www.terraform.io/docs/language/functions/file.html)
- [`sensitive`](https://www.terraform.io/docs/language/functions/sensitive.html)
- [`regex`](https://www.terraform.io/docs/language/functions/regex.html)
- [`contains`](https://www.terraform.io/docs/language/functions/contains.html)

## Howto

You can use functions in any/many places, let's take a look at an example:

### Variables

```hcl
variable "name" {
  type        = string
  description = "The name of the project. It's used to generate unique values for all kinds of resources."
  default     = "my"
  validation {
    condition     = length(var.name) > 0 && length(var.name) <= 32
    error_message = "Please use a name with at least 1 character, and at most 32 characters."
  }
}
```

## Assignment

- [ ] Add a `validation` block to this `variables.tf`:

```hcl
variable "example" {
  type        = string
  description = "Some variable"
}
```

The validation should:

- [ ] Check if the `length` of the input is at least `4` characters, at most `16` characters.
- [ ] Check if the variable `contains` `hello`.
- [ ] Check if the variable only contains lowercase letters

## Questions:

1. Where do you see functions being used? (variables, main, output, providers, versions, etc)
2. Can you share good use of a function from code you already have?

## Solution

```hcl`
variable "example" {
  type        = string
  description = "Some variable"
  default     = "hello there"
  validation {
    condition     = length(var.example) >= 4 && length(var.example) <= 16 && can(regex(".*hello.*", var.example)) && lower(var.example) == var.example
    error_message = "The example variable must be 4 up to 16 characters, contain 'hello' and be lowercase."
  }
}
```
