# Use cases

|expected time|requirements                                             |
|-------------|---------------------------------------------------------|
|120 minutes  |A computer with terraform installed, terraform knowledge.|


Write Terraform code for the cloud provider of your choice.

## Use case 1

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

## Use case 2

## Use case 3
