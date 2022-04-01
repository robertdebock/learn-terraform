# Querying data with output variables

| expected time | requirements                                   |
|---------------|------------------------------------------------|
| 60 minutes    | A computer with Terraform installed.           |

Goal: Learn how to get data from a provider and use it.

## Explanation

Sometimes you need to "read" a detail in order to provision your code. Some example can be:

- Read an already existing VPC.
- Find all availability zones.
- Read the contents of a file.

You may want to use the found data further in your code.

```hcl
# Find all images from a specified family and project.
data "google_compute_image" "my_image" {
  family  = "debian-9"
  project = "debian-cloud"
}

# Make a resource based on the found image.
resource "google_compute_instance" "default" {
  # ...

  boot_disk {
    initialize_params {
      image = data.google_compute_image.my_image.self_link
    }
  }
}
```

Most providers have two sides to a resource:

1. `resource` - To describe the resources to created.
2. `data` - To find resources.

## Demo

[Here](https://github.com/robertdebock/terraform-data).

## Assignment

- For your cloud provider, search for "terraform data {{ PROVIDER }} images". (replace PROVIDER for your provider.)
- Make a new directory, write a `main.tf` to find the images.
- Write a file (`local_file`) with the images found.
