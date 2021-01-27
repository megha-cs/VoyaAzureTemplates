Storage account

**Deploys an Storage Account**



**Example**
```hcl
resource "azurerm_storage_account" "bootstorage" {
    name                        = var.bootstoragename
    resource_group_name         = var.resource_group
    location                    = var.location
    account_replication_type    = var.boot_acc_replication_type
    account_tier                = var.boot_acc_tier
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

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| resource_group             |   The Resource Group for the resources.|String       | n/a       |   yes
| location                   |   The location/region for the resources                              | String      | n/a       |   yes
| boot_acc_replication_type  | The storage account replication type | String | n/a|yes
| boot_acc_tier  | The storage account tier| String | n/a | yes
| bootstoragename  | The storage account name| String | n/a | yes








