1. Create `ssh_config.tf`:

```
resource "local_file" "ssh_config" {
  content  = templatefile("./templates/ssh_config.tpl",
  {
    ip       = azurerm_public_ip.publicip.ip_address,
    username = var.admin_username
   }
   )
    filename = "./ssh_config"
}
```

2. Add `templates/ssh_config.tpl`:

```
Host ${ip}
  User ${username}
```

3. Apply the code:

```
export TF_VAR_admin_password="Password1234!"
export TF_VAR_admin_username="my_username"
```
