# Count

You can add a `count` parameter to resouces, like this:

```hcl
# A simplified example.
resource "azurerm_virtual_machine" "vm" {
  name     = "myTFVM-robert"
  count    = 3
  location = "west europe"
  vm_size  = "Standard_DS1_v2"
}
```

In the example above, the resource is created 3 times.

If you need to refer to one of the (three) instances, you can refer to:

```
# First instance
azurerm_virtual_machine.vm[0]
# Second instance
azurerm_virtual_machine.vm[1]
# Third instance
azurerm_virtual_machine.vm[2]
```

Likely the reference also has a `count` meta argument set, so you can use `count.index`, like this:

```hcl
# A simplified example.
resource "azurerm_virtual_machine" "vm" {
  name     = "myTFVM-robert"
  count    = 3
  location = "west europe"
  vm_size  = "Standard_DS1_v2"
}

# A simplified counted resource example.
resource "azurerm_dns_a_record" "example" {
  name                = "instance-${count.index}"
  count               = length(azurerm_virtual_machine.vm.count)
  zone_name           = azurerm_dns_zone.example.name
  records             = ["10.0.180.17"]
}
```

In the example above, two tricks are used:

1. `count = length(azurerm_virtual_machine.vm.count)`. This takes the `count` from `azure_virtual_machine_vm`. With this construction, you can specify `count` just once, and re-use it over and over again.
2. `name = "instance-${count.index}"`. This `${count.index}` increases by 1 each loop. Be aware, counting starts at `0`.

## Referencing a counted resource.

Imagine you have some resource with a `count` in it:

```hcl
resource "azurerm_virtual_machine" "vm" {
  name     = "myTFVM-robert-${count.index}"
  count    = 3
  location = "west europe"
  vm_size  = "Standard_DS1_v2"
}
```

You would get these machines:

- myTFVM-robert-0
- myTFVM-robert-1
- myTFVM-robert-2

That resource creates `id`. Image you'd like to use that `id` in another resource

```hcl
resource "example_does_not_exist" "example" {
  name     = "something"
  count    = length(azurerm_virtual_machine.vm.count)
  vm_ids      = azurerm_virtual_machine.vm[*].id
}
```

The above is called a `splat` expression.
