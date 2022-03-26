# Console

| expected time | requirements                                              |
|---------------|-----------------------------------------------------------|
| 30 minutes    | A computer with Terraform installed, terraform knowledge. |

Goal: See if using the console can help you.

## Explanation

Using `terraform console` is not an every-day task, but it can be quite useful. The console allows you to:

- Try functions.
- Try to walk over variables.
- Inspect items in the state.

You can access the console by running `terraform console`. Hit CTRL+D to exit.

You can access state to inspect items in the state, just as `terraform show`. In the console you can apply functions to items from the state to see how they react.

### Try function

```text
> length("How long is this string?")
24
```

### Inspect variables

In some (edge) cases, it can be difficult to understand the value of a variable. The console can help.

```text
$ cat variables.tf 
variable "text" {
  default = "Hello world!"
}
$ terraform console
> var.text
"Hello world!"
```

### Inspect state

```text
$ terraform show 
# local_file.default:
resource "local_file" "default" {
    content              = "Hello world!"
    directory_permission = "0755"
    file_permission      = "0644"
    filename             = "foo.bar"
    id                   = "d3486ae9136e7856bc42212385ea797094475802"
}
$ terraform console
> local_file.default
{
  "content" = "Hello world!"
  "content_base64" = tostring(null)
  "directory_permission" = "0755"
  "file_permission" = "0644"
  "filename" = "foo.bar"
  "id" = "d3486ae9136e7856bc42212385ea797094475802"
  "sensitive_content" = (sensitive)
  "source" = tostring(null)
}
> length(local_file.default.content)
12
```

## Assignment

- [ ] Use the [`pow`](https://www.terraform.io/language/functions/pow) function in the console to calculate 4 to the power of 3.
- [ ] From a directory with state, calculate the [`length`](https://www.terraform.io/language/functions/length) of the first resource shown with `terraform show`.
