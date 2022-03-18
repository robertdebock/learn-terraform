# Conditionals

| expected time | requirements                                              |
|---------------|-----------------------------------------------------------|
| 30 minutes    | A computer with Terraform installed, terraform knowledge. |

Goal: Learn how to conditionally create resources.

## Explanation

Sometimes you may want to create a resource on certain conditions. In many other programming languages this will be done using an `if` or `when` statement. In Terraform the syntax is a little weird, so some explanation may help.

## Howto

A conditional is expressed using:

```hcl
condition ? true_val : false_val
```

For example:

```hcl
var.feature ? 1 : 0
```

That would return `1` when `var.feature` is `true`, otherwise `0` is returned.

To optionally create a resource, this conditional can be used on the `count` parameter. That's quite unintuitive:

```hcl
resource "x" "y" {
  count = var.feature ? 1 : 0
  name = "z"
}
```

You can use this `count` trick on `resources` and `data` objects.

You can test quite some things/conditions, here are some examples:

```hcl
# Compare a string:
var.variable == "something" ? 1 : 0

# Negative compare:
var.variable != "something ? 1 : 0

# You can also return some value on a condition. (That would not be in the `count` parameter.)
var.variable == "europe" ? "amsterdam": "other"

# Or compare a value:
var.variable > 10 ? "large" : "small"

# Or use a function:
regex('pattern', var.variable) ? "found" : "not found"
```

## Assignment

1. Write (pseudo) code to:
- Define a variable `my_var`.
- Create a resource `example`.
- Make the `example` resource conditionally, when `my_var` is an odd number.

Here are some hints:

- Check the [`variable`](https://www.terraform.io/language/values/variables) documentation.

```hcl
resource "example" "default" {
  name = "whatever"
}
```

- Odd numbers can be tested with the ['%' operator](https://www.terraform.io/language/expressions/operators).

## Questions:

Can you explain these conditionals:

```hcl
count = var.vpc_id == "" ? 1 : 0
```

```hcl
count = var.vpc_id == "" ? min(length(data.aws_availability_zones.default.names), var.amount) : 0
```

```hcl
count = var.vpc_id != "" && var.bastion_host ? 1 : 0
```

## Solution

```hcl
variable "my_var" {
  type = number
}

resource "example" "default" {
  count = var.my_var % 2 != 0 ? 1 : 0
  name = "whatever"
}
```
