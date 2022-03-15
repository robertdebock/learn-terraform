# Ordering

The order of objects (`resource`, `data`, `variable`, `output`, `locals` or any other object) is technically not relevant. You can put any object in any `.tf` file.

There is an order that is nice for humans. Making a decision help to make a repository more maintainable.

## Dependency oriented

In this order, you describe the object that's reused later, first:

```hcl
resource "x" "foo" {
  name = "bar"
}

resource y "bar" {
  name = "foo"
  relation = x.foo.id
}
```

This means that the top of the file contains resources without a relation, where the bottom likely has resources that depend on above resources.

## Architecture oriented

In this order, you keep in mind how the architecture is used. For example:

```hcl
resource "dns_record" "default" {
  name  = "www"
  value = loadbalancer.default.ip
}

resource "loadbalancer" "default" {
  name = "bar"
}
```

## Bottom-up oriented

In this order, you describe the resource that provides a service first, and introduce depending resources later. The Terraform documentation for GCP uses this ordering frequently.

```hcl
resource "instance" "default" {
  name    = "x"
  network = network.default.id
  volume  = volume.default.id
}

resource "network" "default" {
  name = "y"
}

resource "volume" "default" {
  name = "z"
  size = "23G"
}
```
