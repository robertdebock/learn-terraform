# tfenv

| expected time | requirements                                              |
|---------------|-----------------------------------------------------------|
| 15 minutes    | A computer with Terraform installed, terraform knowledge. |

Goal: Learn how to benefit from tfenv.

## Explanation

`tfenv` is a tool to manage versions of Terraform. It can be useful to quickly download or select a new version of Terraform. This would be useful for developing Terraform code and testing if it works on multiple versions of Terraform.

## Howto

You may need to [install](https://github.com/tfutils/tfenv) tfenv. On the lab-machines it's ready to be used.

Once installed you can:

- List locally installed versions: `tfenv list`.
- List remotely available versions: `tfenv list-remote`.
- Install new Terraform versions: `tfenv install 1.1.7`.
- Select Terraform versions: `tfenv use 1.1.7`.
- Install the latest Terraform version: `tfvar install latest`.
- Install the minimum required Terraform version: `tfvar install min-required`.

You can also pick a version in `.terraform-version`.

## Assignment

1. What version of Terraform do you have installed now?
2. Install a very old version (`0.6.1`) of Terraform, see if your code still works.
3. Update to the latest version of Terraform.

## Questions:

- Where or how could you use `tfenv` in your environment?
