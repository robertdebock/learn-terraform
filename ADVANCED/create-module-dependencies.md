# Create module dependencies

| expected time | requirements                                   |
|---------------|------------------------------------------------|
| 60 minutes    | A computer with Terraform installed.           |

Goal: Learn how module dependencies work in Terraform.

## Explanation

Using modules make the root-module much easier to read, so you'll likely end up writing and/or using modules.

Modules can depend on each other since Terraform 0.13. (August 2020)

## Howto

You can simply use `depends_on` for an explicit dependency or refer to `module.NAME.OUTPUT`.

## Demo

Have a look at this [experiment](https://github.com/robertdebock/terraform-module-dependencies)

## Assignment

- [ ] Create a new directory for your expiment.
- [ ] In that directory, create these directories: `network`, `instance`.
- [ ] In `network` directory, create a `main.tf` to create the [network](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_network).
- [ ] Make sure the `network` module [outputs](https://www.terraform.io/language/values/outputs) the network `id`.
- [ ] In the `instance` directory, create a `main.tf` to create the [instance](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_instance).
- [ ] The `instance` module needs a [variable](https://www.terraform.io/language/values/variables) to describe the [network](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_instance#network) this instance should live in.
- [ ] In `instance/main.tf`, make sure to use the `var.network` created in the step above.
- [ ] Create `main.tf` in the root-module, calling both the `./network` and `./instance` module.
- [ ] Create an implicit dependency from module `instance` to the module `network`, by mentioning the `module.network.id` as input for the `instance` module.

## Questions

1. Are there differences in dependencies on resources and modules?
2. In the [example experiment](https://github.com/robertdebock/terraform-module-dependencies); The dependency between module `one` and `two` is based on a (hidden, not exposed) artefact. How would you rewrite the code to make this dependency visible?
 
## Notes

If you need to set an explicit dependency, reconsider if you are [doing it wrong](https://cdn.quotesgram.com/img/23/91/2020555313-Boating_-you_re-doing-it-wrong.jpg).
