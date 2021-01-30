# Organization

The files you place in a repository can be split up. [Hashicorp](https://www.terraform.io/docs/language/modules/develop/structure.html) documents this, here is a summary.

```tree
.
├── examples
│   └── default
│       └── main.tf
├── LICENSE
├── main.tf
├── outputs.tf
├── README.md
├── variables.tf
└── versions.tf
```

You could even introduce a `providers.tf` to split provider specific details in.

The intent of the splitting is that you and others can easily find how to use the role.
