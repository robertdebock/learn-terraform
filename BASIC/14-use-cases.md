# Use cases

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|120 minutes  |A computer with Terraform installed, terraform knowledge.|

Goal: Write Terraform code for the cloud provider of your choice.

## Explanation

We'll try some experiments. Some of these experiments take some time to finish, maybe you'll run into issues. Don't worry, share your screen to troubleshoot together.

Pick the easiest use case first.

## Howto

### Use case 1

Use [cloud-init](https://cloudinit.readthedocs.io/en/latest/) in the Terraform code ([hint](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_machine#custom_data) to do these things on a newly generated system:

- Add a group "my-users".
- Add a user "my-user" that:
  - Belongs to the group "my-users".
  - Has a password of "My-P@s5w0rd". (use a hash `mkpasswd --method=SHA-512 --rounds=4096`)
  - Can use sudo (`sudo:  ALL=(ALL) NOPASSWD:ALL`).
- Update the software on the instance. ([hint](https://cloudinit.readthedocs.io/en/latest/topics/examples.html#update-apt-database-on-first-boot).)

- [solution](https://github.com/robertdebock/learn-terraform-azure/tree/cloudinit).

### Use case 4

Add a resource manually, import and try to expand the memory.

- [Solution](14-use-cases-solution-import.md)

### Use case 3

How do you organize variables so that you have the least amount of locations to define variables, but keep flexibility.

For example:

- [ ] The `location` where resources are provisioned is fixed for the company.
- [ ] The `size` of a VM has a suggested value, but can be overwritten.
- [ ] The `name` of a VM should be given by the user of the module.
- [ ] A list of subscriptions (and their id), where different environments use specific subscriptions.

- [Solution](14-use-cases-solution-organizing.md)

### Use case 4

Write Terraform code to:

```text
        +--- loadbalancer1 ---+
        | Listening on ports: |
        |   - port 80         |
        |   - port 443        |
        +---------------------+
               |         |
               V         V
+--- instance1 ---+   +--- instance2 ---+
| Linux:          |   | Linux:          |
|   - apache      |   |   - apache      |
+-----------------+   +-----------------+
```

The image above leaves some room for interpretation. If you're done, you should be able to:

1. Visit the IP address of the loadbalancer in your browers.
2. Get service a page (likely default) from `instance1` or `instance2`.

### Use case 5

You've written Terraform code, see what items can be moved to a module and rewrite your code to use these modules.

## Questions
