# Azure Static website with CDN Endpoint

Configuration in this directory creates Azure storage account and enable the static website and create optional CDN service for the static website.

## Module Usage

## Static Website

Following example to create a storage account with static website.

```hcl
module "static-website-cdn" {
  source  = "kumarvna/static-website-cdn/azurerm"
  version = "2.0.0"

  # Resource Group, location, and Storage account details
  resource_group_name  = "rg-demo-westeurope-01"
  location             = "westeurope"
  storage_account_name = "storageaccwesteupore01"

  # Static Website createion set to true by default
  # account_kind should set to StorageV2 or BlockBlobStorage
  static_website_source_folder = var.static_website_source_folder
  index_path                   = var.index_path
  custom_404_path              = var.custom_404_path

  # Adding TAG's to your Azure resources (Required)
  tags = {
    Terraform   = "true"
    Environment = "dev"
    Owner       = "test-user"
  }
}
```

## Static Website with CDN endpoint

Following example to create a storage account, static website with CDN endpoint.

```hcl
module "static-website-cdn" {
  source  = "kumarvna/static-website-cdn/azurerm"
  version = "2.0.0"

  # Resource Group, location, and Storage account details
  resource_group_name  = "rg-demo-westeurope-01"
  location             = "westeurope"
  storage_account_name = "storageaccwesteupore01"

  # Static Website createion set to true by default
  # account_kind should set to StorageV2 or BlockBlobStorage
  static_website_source_folder = var.static_website_source_folder
  index_path                   = var.index_path
  custom_404_path              = var.custom_404_path

  # CDN endpoint for satic website
  enable_cdn_profile = true
  cdn_profile_name   = var.cdn_profile_name
  cdn_sku_profile    = var.cdn_sku_profile

  # Adding TAG's to your Azure resources (Required)
  tags = {
    Terraform   = "true"
    Environment = "dev"
    Owner       = "test-user"
  }
}
```

## Terraform Usage

To run this example you need to execute following Terraform commands

```hcl
terraform init
terraform plan
terraform apply
```

Run `terraform destroy` when you don't need these resources.

## Outputs

Name | Description
---- | -----------
`static_website_cdn_endpoint_hostname` | CDN endpoint URL for Static website
`static_website_cdn_profile_name` | CDN profile name for the static website
`static_website_url` | static web site URL from storage account
`storage_account_id` | The ID of the storage account
`storage_account_name` | The name of the storage account
`storage_primary_access_key` | The primary access key for the storage account
`storage_primary_connection_string` | The primary connection string for the storage account
