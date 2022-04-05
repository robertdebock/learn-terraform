# Troubleshooting

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|15 minutes   |A computer with Terraform installed, terraform knowledge.|

Goal: Troubleshoot Terraform issues.

## Explanation

Sometimes you may need to understand what Terraform does in order to understand what goed wrong.

Typically this happens with less mature providers. The commonly used providers are pretty stable and no not need a lot of troubleshooting.

## Howto

Terraform runs quietly normally. You can increase debugging by setting `TF_LOG` to `TRACE` or `DEBUG`.

```
TF_LOG=DEBUG terraform apply
```

To save the output, use `TF_LOG_PATH`.

```
TF_LOG=DEBUG TF_LOG_PATH="./DEBUG.txt" terraform apply
```

Crashlogs (`crash.log`) can be use to let HashiCorp troubleshoot issues.

Sometimes, you may want to see some data. With failing builds this can be a challenge. Here is a trick to inspect data.

```hcl
resource "null_resource" "terraform-debug" {
  provisioner "local-exec" {
    command = "echo $VARIABLE1 >> debug.txt ; echo $VARIABLE2 >> debug.txt"

    environment = {
        VARIABLE1 = jsonencode(var.your_variable_name)
        VARIABLE2 = jsonencode(local.piece_of_data)
    }
  }
}
```

The above code has no dependencies (except for the varialbe and local) so will execute early. This means you can inspect variables, locals, but also created resources. (Although that would introduce a dependency...)

## Assignment

- [ ] Run a plan and save the debugging output to `debug-output.txt`.

## Questions

1. As experienced Terraform users, did you ever have the need to debug?
2. Where can you ask for help if Terraform gives you issues?

## Solution

Not difficult, but see [here](troubleshooting-solution.md).
