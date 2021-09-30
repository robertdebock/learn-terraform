# Build a virtual machine scale set

|expected time|requirements|
|-------------|------------|
|60 minutes   |a computer  |

Goal: Experiment with a Virtual Machine Scale Set.

## Explanation

A scale set allow you to treat a set of machines as one resource. Typically a loadbalancer sends traffic to healthy members of a scale set.

A scaleset is easier to maintain than individual VM's, for example; a single number (`instances`) can scale up (or down) the amount of machines in a scale set.

A scaleset can also manage it's own capacity (number of instances in the scale set) using a [`monitoring_autoscale_setting`](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/monitor_autoscale_setting) resource.

## Howto

Have a look at the [terraform documentation on scale sets](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_machine_scale_set).

There are quite some parameters to set; you may need to search for a few examples.

## Demo

See this [azure linux virtual machine](https://github.com/robertdebock/terraform-azurerm-scale-set) example.

A nice feature of the code above is that it uses [cloud-init](https://cloudinit.readthedocs.io/en/latest/) to customize the instance. An alternative would be to make an image using a tool as [packer](https://www.packer.io/).

## Assignment

- [ ] Write the Terraform code to provision a scale set. Likely begin with the example mentioned in the demo.
- [ ] Ensure that the scale-set starts with 3 nodes.
- [ ] Ensure that the autoscaling minimum instances is set to 2 nodes.
- [ ] Ensure that the autoscaling maximum instances is set to 5 nodes.
- [ ] Visit the [Azure Portal](https://portal.azure.com/) to review your work. (All resources -> Virtual machine scale set -> Scaling -> Run history)

Bonus: (Only if you have extra time)

- [ ] Add SSL (httpd) to apache2. [Here](https://www.informaticar.net/enable-https-on-ubuntu-web-server-20-04/) are some hints.
- [ ] Also forward traffic to port 443 to the instances.

## Questions

1. With Terraform, there is a `count` parameter for resources. Instead of a linux_virtual_machine_scaleset, you could also just add `count` to a linux_virtual_machine resource. What are the benefits of a scale-set?
2. Imagine you need to troubleshoot the instances, how would you connect?
