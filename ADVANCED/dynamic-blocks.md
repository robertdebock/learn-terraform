# dynamic blocks

| expected time | requirements                                              |
|---------------|-----------------------------------------------------------|
| 45 minutes    | A computer with Terraform installed, terraform knowledge. |

Goal: See how you may use Terraform dynamic blocks.

## Explanation

Sometimes you want to loop over a list and repeat a "block". For example tcp-ports that should be allowed to access a resource.

This can be a challenge because the looping need to happen in a resource. Think if this example:

```hcl
resource "x" "y" {
  name = "my-thing"
  allow {
    port = 80
  }
  allow {
    port = 443
  }
}
```

It's anoying to repeat this `allow` block. Dynamic blocks to the rescue!

## Howto

With the `resource` and `variable`s as described above, you can use a dynamic block:

```hcl
variable "allow" {
  default = [
    {
      port = 80
    },
    {
      port = 443
    }
  ]
}

resource "x" "y" {
  name = "my-thing"
  dynamic "allow" {
    for_each = var.allow
    content {
      port = allow.value.port
    }
  }
}
```

Dynamic blocks are required from time to time, but a person less terraform-skilled may find this construct difficult to understand.

You can use blocks-in-blocks, making the code even harder to read.

## Demo

Have a look [here](https://github.com/robertdebock/terraform-gcp-dynamic-block).

## Assignment

1. Find a resource with a repeating block in it. Here are some suggestions:

- [bigquery_dataset](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_dataset).
- [pubsub_topic](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/pubsub_topic).
- [compute_instance_group](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_instance_group).
- Or any other that you know or can find.

2. Write the resource, but replace the repeating block with a `dynamic block`.
3. Add a variable to pass the values used in the `dynamic_block`.

## Questions

1. Is there currently any (root) module in use that can benefit from a `dynamic block`?
