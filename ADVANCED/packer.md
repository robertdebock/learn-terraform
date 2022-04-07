# Packer

|expected time|requirements                 |
|-------------|-----------------------------|
|60 minutes   |A computer with az installed.|

Goal: Understand how to create images to spin up instances.

## Explanation

So far we've used images created by the cloud provider. Typically these images work, but sometimes extra configuration is required, think if these things:

- A hardened image.
- An image with executables pre-installed.
- An image with self-registration capabilities.
- An image of a specific Linux distribution.

In those situations it can be useful to create your own image using [Packer](https://www.packer.io/).

## Howto

Let's go over the [Azure README.md](https://github.com/robertdebock/packer-azure-arm/blob/master/README.md) or [GCP README.md](https://github.com/robertdebock/packer-gcp-centos/blob/master/README.md).

## Assignment

- [ ] Azure: Clone [this](https://github.com/robertdebock/packer-azure-arm) repository.
- [ ] GCP: Clone [this](https://github.com/robertdebock/packer-gcp-centos) repository.
- [ ] Install [Packer](https://www.packer.io/).
- [ ] Follow the steps in the [Azure README.md](https://github.com/robertdebock/packer-azure-arm/blob/master/README.md) or [GCP README.md](https://github.com/robertdebock/packer-gcp-centos/blob/master/README.md) to build an image.
- [ ] Azure Bonus: `16.04-LTS` is a bit old. Find a newer `sku`.
- [ ] GPC Bonus: Make the script nicer, add some `/etc/motd`, packages, services, etc.

## Questions

1. Would building images be something for your organization?
2. Conceptually, can I build an Amazon image on Azure or GCP?

## Solution

See [ubuntu.json](https://github.com/robertdebock/packer-azure-arm/blob/master/ubuntu.json)

## Hints

- Find images using `az vm image list --all --publisher Canonical`.
