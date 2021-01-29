# Troubleshooting

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|90 minutes   |A computer with Terraform installed, terraform knowledge.|

Troubleshoot Terraform issues.

## Explanation

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

## Questions

## Solution
