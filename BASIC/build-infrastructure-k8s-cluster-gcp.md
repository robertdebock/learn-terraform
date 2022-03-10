# Build infrastructure K8s cluster (GCP)

|expected time|requirements|
|-------------|------------|
| 60 minutes  | a computer |

Goal: Learn how to create a K8s cluster on GCP using Terraform.

## Explanation

A Kubernetes cluster consists of many components. Creating one "manually" is time consuming and error prone.

Using Terraform to deploy a k8s cluster is quite simple.

## Howto

Use [`google_container_cluster`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/container_cluster) to setup a K8s cluster. The documentation is a great starting point.

## Demo

See [this example repository](https://github.com/robertdebock/terraform-gcp-kubernetes-cluster/blob/master/main.tf).

## Assignment

|----------|--------------|
| beginner | intermediate |
| Have a look at the [sample repository](https://github.com/robertdebock/terraform-gcp-kubernetes-cluster/blob/master/main.tf), clone it, and follow the steps in the README.md. | You'll manually write Terraform code. Uses these resources. |
|          | 1. `google_compute_network` |
|          | 2. `google_compute_subnetwork` |
|          | 3. `google_container_cluster` |
|          | 4. `google_container_node_pool` |

## Questions

1. What would be a realistic `node_count`?
2. Why are there 6 nodes, even though `gke_num_nodes` is set to `2`.
2. What [`vm_size`](https://docs.microsoft.com/en-us/azure/virtual-machines/sizes) would be good?
3. Was the cluster updated or recreated when changing the `machine_type`?
4. Was the cluster updated or recreated when changing the `gke_num_nodes`?
