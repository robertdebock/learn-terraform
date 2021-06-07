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

## Assignment

- [ ] Run a plan and save the debugging output to `debug-output.txt`.

## Questions

1. As experienced Terraform users, did you ever have the need to debug?
2. Where can you ask for help if Terraform gives you issues?

## Solution

Not difficult, but see [here](troubleshooting-solution.md).
