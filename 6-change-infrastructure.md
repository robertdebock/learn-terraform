# Change infrastructure

|expected time|requirements                                    |
|-------------|------------------------------------------------|
|30 minutes   |A computer with terraform installed, lab 5 done.|

Learn how to change infrastructure:

- [AWS](https://learn.hashicorp.com/tutorials/terraform/aws-change?in=terraform/aws-get-started).
- [Azure](https://learn.hashicorp.com/tutorials/terraform/azure-change?in=terraform/azure-get-started).
- [GCP](https://learn.hashicorp.com/tutorials/terraform/google-cloud-platform-change?in=terraform/gcp-get-started).

In this case it's nice to see your changes in the provider console:

- [AWS](https://aws.amazon.com/console/).
- [Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups).
- [GCP](https://console.cloud.google.com/).


# Questions:

1. Can I still change stuff (resources) manually on the providers console?
2. If I lost the state file, can I simply re-apply the same Terraform code?
3. If I change the name of an instance, will the instance be recreated or renamed?
4. Why would you append `-out=planfile` to `terraform plan`?
