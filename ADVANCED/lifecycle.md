# lifecycle

| expected time | requirements                                              |
|---------------|-----------------------------------------------------------|
| 60 minutes    | A computer with Terraform installed, terraform knowledge. |

Goal: Be able to decide when to use the `lifecycle` meta argument and implement it.

## Explanation

In some situations, Terraform needs to destroy and create a resource on changes. This means services may be interrupted. the `lifecycle` meta argument can prevent this.

Be aware that you need to prevent conflicts in names of resources, ports, and likely other parameters.

This type of deployment is ofter referred to as [blue-green deployment](https://en.wikipedia.org/wiki/Blue-green_deployment).

## Howto

See [this demo](https://github.com/robertdebock/terraform-docker-lifecycle)

## Assignment

- [ ] Go back to the [Azure container groups](https://github.com/robertdebock/terraform-azurerm-container-group) repository, clone the code to your computer.
- [ ] Add a `variables.tf` to define a variable like `deployment` or so.
- [ ] Introduce the [`lifecycle`](https://www.terraform.io/docs/language/meta-arguments/lifecycle.html) meta argument to `main.tf`
- [ ] Change the `azurerm_container_group.example.name` to use the variable defined in `variables.tf`.
- [ ] Change the `azurerm_container_group.example.dns_name_label` to use the variable defined in `variables.tf`.
- [ ] Run the deployment and add `-var="deployment=1"`.
- [ ] Run the deployment and add `-var="deployment=2"`.
- [ ] Run the deployment and add `-var="deployment=1"`.

## Questions

1. Was the service interrupted during the deployments?
2. The deployment resulted in exposing a new IP address, how could you use this mechanism to make an uninterrupted deloyment?
3. How much time was saved in the below example?

```text
azurerm_container_group.example: Creating...
azurerm_container_group.example: Still creating... [10s elapsed]
...
azurerm_container_group.example: Still creating... [1m10s elapsed]
azurerm_container_group.example: Creation complete after 1m16s [id=/subscriptions/27c6a60b-0aed-4e75-a7ea-f5cf2e49f89e/resourceGroups/example-resources/providers/Microsoft.ContainerInstance/containerGroups/example-continst-2]
azurerm_container_group.example: Destroying... [id=/subscriptions/27c6a60b-0aed-4e75-a7ea-f5cf2e49f89e/resourceGroups/example-resources/providers/Microsoft.ContainerInstance/containerGroups/example-continst]
azurerm_container_group.example: Still destroying... [id=/subscriptions/27c6a60b-0aed-4e75-a7ea-...tance/containerGroups/example-continst, 10s elapsed]
...
azurerm_container_group.example: Still destroying... [id=/subscriptions/27c6a60b-0aed-4e75-a7ea-...tance/containerGroups/example-continst, 1m10s elapsed]
azurerm_container_group.example: Destruction complete after 1m13s
```

## Solution

- See this [lifecycle branch](https://github.com/robertdebock/terraform-azurerm-container-group/tree/lifecycle).

## Sources

- [lifecycle](https://www.terraform.io/docs/language/meta-arguments/lifecycle.html)
