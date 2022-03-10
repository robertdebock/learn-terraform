# Structures

A bit of information on the different type of data structures in Terraform.

## String

This is the simplest form, for example:

```hcl
hello = "world"
```

Here the variable `hello` is filled with the value `world`.

By the way, in a .tf file, if you quote a value, it's literally that value. Without quotes would be a reference. For example:

```hcl
hello = resource.identifier.id
```

Would assign the value of `resource.identifier.id` to the varialbe `hello`.

## Number

Almost like a string, but not quoted and numeric:

```hcl
value = 123
other_value = 123.123
```

You can do arithmetic operations with numbers:

```hcl
value = 2
other_value = "${var.value * 3}"
```

## Boolean

May look like an unquoted string, but can only be `true` or `false`:

```hcl
enable_feature_x = true
enable_feature_y = false
```

## List

A list is a sequence of values. For example:

```hcl
hello = ["one", "two", "world"]
```

A list typically contains "similar" items.

## Map or dictionary

A map, mapping or dictionary (different words for the same concept) looks like this:

```hcl
hello = {
  one = "hello"
  two = "world"
}
```

(Just like a dictionary that has some word and an explanation.)

Mappings can be used to map a value like so:


```hcl
city = "paris"

_region = {
  amsterdam = "eu-west-1"
  paris     = "eu-central-1"
  oslo      = "eu-north-1"
}

region = _region[city]
```

NOTE: The above example won't work, as these structures should be in a variable (`var.something`) or a local (`local.something`). It's just to explain then concept.

## Combinations

You can also have lists of maps: (or actually any kind of structure.)

```hcl
list = [
{
  some = "thing"
},
{
  other = "things"
}
]
```

## Simplicity ordering

(A bit opinionated...)

From simple to complex:

1. boolean - Can only be `true` or `false`.
2. number - Can only be a number, with or without a decimal point.
3. string - Can be a sequence of characters.
4. list - Can be a list of strings, maps, numbers or even list.
5. map - Just like list, can contain anything.

## Advice

1. Try to use the simplest structure.
2. For user-facing structures: keep it as simple as possible.
