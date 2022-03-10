# Organization

|expected time|requirements|
|-------------|------------|
| 30 minutes  | a computer |

Goal: Understand how to best organize Terraform repositories.

## Explanation

The files you place in a repository can be split up. [Hashicorp](https://www.terraform.io/docs/language/modules/develop/structure.html) documents this, here is a summary.

## Howto

```tree
.
├── examples
│   └── default      # <- You can have other scenarios as well.
│       └── main.tf  # <- This is a root-module, using this module.
├── LICENSE
├── main.tf          # <- Here is where you store "logic".
├── outputs.tf       # <- The output is described here.
├── README.md
├── variables.tf     # <- The input is described here.
└── versions.tf      # <- Uses providers/modules go heere.
```

You could also introduce a `providers.tf` to split provider specific details in.

The intent of the splitting is that you and others can easily find how to use the role.

## Demo

## Assignment

- [ ] Split the files in your repository into the files described above.

## questions

- [ ] Can you use `inputs.tf` instead of `variables.tf`?
