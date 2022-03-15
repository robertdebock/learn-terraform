# Build a compute autoscaler

|expected time|requirements|
|-------------|------------|
| 60 minutes  | a computer |

Goal: Experiment with a Google Compute Autoscaler.

## Explanation

A compute autoscaler allow you to treat a set of machines as one resource. Typically a load balancer sends traffic to healthy members of a compute autoscaler.

A compute autoscaler is easier to maintain than individual VM's, for example; a single number (`instances`) can scale up (or down) the amount of machines in a compute autoscaler.

A computer autoscaler can also manage it's own capacity (that's the number if instances) using a `autoscale_policy`.

## Howto

Have a look at the [terraform documentation on compute autoscalers](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_autoscaler).

There are quite some parameters to set; you may need to search for a few examples.

## Demo

See this [gcp computer autoscaler](https://github.com/robertdebock/terraform-gcp-compute-autoscaler) example.

A nice feature of the code above is that it uses [cloud-init](https://cloudinit.readthedocs.io/en/latest/) to customize the instance. An alternative would be to make an image using a tool as [packer](https://www.packer.io/).

## Assignment

- [ ] Start with the [example](https://github.com/robertdebock/terraform-gcp-compute-autoscaler).
- [ ] Set the `min_replicas` to 2.
- [ ] Set the `max_replicas` to 5.
- [ ] Login to (2) instances and run `yes > /dev/null`. This generates load.
- [ ] Wait until the `cpu_utilization.target` is above 70% and new instances are stared.

Bonus:
- [ ] Build a load balancer on front of the machines.

## Questions

1. With Terraform, there is a `count` parameter for resources. Instead of a `google_compute_autoscaler`, you could also just add `count` to a `google_compute_instance` resource. What are the benefits of a scale-set?
2. Does terraform know of the instances that the `google_compute_autoscaler` has generated?
