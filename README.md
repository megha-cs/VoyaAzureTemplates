Linux_VM

**Deploys an Linux VM**


**Example**
```hcl
resource "azurerm_linux_virtual_machine" "server" {
  name                            = upper(var.servername)
  resource_group_name = var.resource_group
  location            = var.location
  size                = var.sku
  admin_username      = lower(var.servername)
  network_interface_ids = [azurerm_network_interface.nic.id,]
  availability_set_id    = var.availability_set_id
  provision_vm_agent    = true
  source_image_id = var.source_image_id
  zone                  = var.zone
  admin_ssh_key {
    username   = lower(var.servername)
    public_key = "${tls_private_key.example_ssh.public_key_openssh}"
}
  os_disk {
    name                 = "${upper(var.servername)}-OsDisk1"
    caching              = "ReadWrite"
    storage_account_type = var.os_storage_account_type
    disk_size_gb         = var.os_disk_size_gb
  }
  boot_diagnostics {
    storage_account_uri = var.boot_diag_storage_uri
    }
   tags = var.tags
    lifecycle {
    ignore_changes = [
      tags,
      admin_username,
      admin_ssh_key,
      identity,
      os_disk, 
    ]
  }
}
```

## Requirements

| Name | Version |
|------|---------|
| terraform | >= 0.12.26 |
| azurerm | >= 2.4.0 |

## Providers

| Name | Version |
|------|---------|
| azurerm | >= 2.4.0 |

**Inputs**
| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| resource_group             |   The Resource Group for the resources.|String       | n/a       |   yes
| location                   |   The location/region for the resources                              | String      | n/a       |   yes
| subnet_id                  |    The Subnet id for NIC.                                            |  String     |  n/a      |    yes
| servername                 |    The Name of the Server.                                           |  String     |  n/a      |     yes
| sku                        |    Virtual machine SKU                                               |  String     |  n/a      |     yes
| os_storage_account_type    |    OS Disk storage sku                                               |  String     |  n/a      |     yes
| zone                       |    Availability zone for the resource to be created in               |  String     |  n/a      |     no
| os_disk_size_gb            |    Enables data disk creation                                        |  number     |  n/a      |     yes
| availability_set_id        |    Id of the availability set                                        |  String     |  n/a      |     no
| source_image_id            |    The ID of an Image which each Virtual Machine should be based on  |  String     |  n/a      |     yes
| data_disks                 |    Map of object of disk sizes                                       |  Map        |  n/a      |     no
| create_data_disk           |   Enables data disk creation                                         | String      | n/a       |    no
| tags                       |    A map of tags to add to all resources                             |  Map/String | n/a       |    no
| boot_diag_storage_uri      |    Storage account URI for Boot Diagnostics.                         |  String     |  n/a      |     yes
| key_vault_id               |    The KeyVault ID to store SSH keys                                 |  String     |  n/a      |     no
| dependancyAgent            |    Enables dependecy agent for Azure Monitor                         |  string     |  n/a      |     no
| install_oms_agent          |    Installs OMS agent for Log Analytics                              |  String     |  n/a      |     no
| log_analytics_workspace_id  |   ID for Log Analytics Work space.                                  |  String     |  n/a      |    no
| log_analytics_workspace_key  |  Log Analytics access key                                          |  String     |  n/a      |     no




**Outputs**

| Name | Description |
|------|-------------|
| vm_id   | Virtual machine ids created |
| vm_name | Virtual machine name created |
| network_interface_ids | ids of the vm nics provisoned |
| network_interface_private_ip | private ip addresses of the vm nics |




