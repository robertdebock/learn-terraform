# Define input variables

|expected time|requirements                                    |
|-------------|------------------------------------------------|
|60 minutes   |A computer with Terraform installed.            |

Goal: Learn how to define input variables.

## Explanation

![input output](images/input-output.png "Input Output")

Besides the code to build the infrastructure, you may need to have some details that are required to build the infrastructure. You can use Terrafor input variables.

Examples of input are:

- The amount of machines required.
- The name of a machine.
- The size of an instance.
- (and many more.)

## Howto

Follow the steps described for your cloud provider.

- [AWS](https://learn.hashicorp.com/tutorials/terraform/aws-variables?in=terraform/aws-get-started).
- [Azure](https://learn.hashicorp.com/tutorials/terraform/azure-variables?in=terraform/azure-get-started).
- [GCP](https://learn.hashicorp.com/tutorials/terraform/google-cloud-platform-variables?in=terraform/gcp-get-started).

## Demo

## Assignment

- [ ] Follow the `Howto` for your provider.

## Questions:

1. Why is the command line a best practice location for specifying sensitive variables?
2. What would be one or more drawbacks of not using variables?
3. Can I list my variables in `input.tf` instead of `variables.tf`?
