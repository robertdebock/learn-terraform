# Build infrastructure K8s cluster

|expected time|requirements|
|-------------|------------|
|60 minutes   |a computer  |

Goal: Learn how to create Azure K8s resources on Azure using Terraform.

## Explanation

A Kubernetes cluster consists of many components. Creating one "manually" is time consuming and error prone.

Using Terraform to deploy a `azurerm_kubernetes_cluster` resource is quite simple.

## Howto

Use [`azurerm_kubernetes_cluster`](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/kubernetes_cluster) to setup a K8s cluser. The documention is a great starting point.

## Demo

See [this example repository](https://github.com/robertdebock/terraform-azurerm-kubernetes-cluster).

## Assignment

Use the sample code above and change these settings:

- [ ] Use the default as described in the [documentation](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/kubernetes_cluster).
- [ ] Spin up the K8s cluster.
- [ ] Change the VM size from `Standard_D2_v2` to `Standard_D4_v2`.
- [ ] Apply the code again.
- [ ] Make sure the cluster has a `node_count` of `3`.
- [ ] Apply the code once mode.

## View the results

| [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups)|

## Questions

1. What would be a realistic `node_count`?
2. What [`vm_size`](https://docs.microsoft.com/en-us/azure/virtual-machines/sizes) would be good?
3. Was the cluster updated or recreated when changing the `vm_size`?
4. Was the cluster updated or recreated when changing the `node_count`?
