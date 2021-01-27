# Input validation

Input can be limited to `type`, but that only defines the desired type of input, one of:

- `string`
- `number`
- `bool`
- list(<TYPE>)
- set(<TYPE>)
- map(<TYPE>)
- object({<ATTR NAME> = <TYPE>, ... })
- tuple([<TYPE>, ...])

These types do not tell anything about the validity of the value that's set.

Validating the input variables given can help a consumer of the role.

You can even do some light-weight policies in modules.

```hcl
variable "name" {
  type        = string
  description = "Some description"

  validation {
    condition     = length(var.image_id) > 4 && substr(var.image_id, 0, 3) == "my-"
    error_message = "The name must start with \"my-\", and be at least 4 characters long."
  }
}
```
