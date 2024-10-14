---

copyright:
  years: 2023, 2024
lastupdated: "2024-10-11"

keywords: app-configuration, app configuration, tutorials, terraform, infrastructure as code, iac, terraform provider

subcollection: app-configuration

content-type: tutorial
account-plan: standard
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}

# Working with Terraform in {{site.data.keyword.appconfig_short}}
{: #ac-tera-workwith}
{: toc-content-type="tutorial"}
{: toc-completion-time="30m"}

This tutorial shows you how to use Terraform to configure files like `provider.tf` to declare {{site.data.keyword.appconfig_short}} resources for deployment.
{: shortdesc}

## Before you begin
{: #ac-prereqs-terraform}

Ensure that the following prerequisites are in place:

* Install Terraform. For more information, see [Download Terraform](https://developer.hashicorp.com/terraform/install){: external}.
* Either deploy Terraform to a specific folder or add it to your `PATH`.

* Check your version of Terraform:

   ```bash
   terraform –version
   ```
   {: codeblock}

* You need an {{site.data.keyword.cloud_notm}} account. If you don't have an account, then [Create an IBM Cloud account](https://cloud.ibm.com/registration/){: external}.
* Log in to your {{site.data.keyword.cloud_notm}} account.
* Connect to your {{site.data.keyword.cloud_notm}} account with {{site.data.keyword.cloud_notm}} API Key.
* Login to [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/login){: external} and go to the **Manage** tile and select **Access(IAM)**, and then select **{{site.data.keyword.cloud_notm}} API Keys**.
* Create an {{site.data.keyword.cloud_notm}} API Key and save the password.
* For more information about the terraform provider plug in, see [Installing the IBM Cloud Provider plug-in](https://cloud.ibm.com/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install_provider){: external}

## Building Infrastructure-as-Code
{: #ac-infrastructure-as-code}
{: step}

Create a `tf-template` directory that contains the following Terraform configuration files:

### `provider.tf`
{: #ac-provider-tf}

`provider.tf` creates the required providers.

```hcl
terraform {
   required_providers {
      ibm        = {
         source  = "IBM-Cloud/ibm"
         version = "1.57.0"
      }
   }
}
```
{: codeblock}

### `instance.tf`
{: #ac-instance-tf}

`instance.tf` provisions an {{site.data.keyword.appconfig_short}} instance.

```hcl
resource "ibm_resource_instance" "terraform_demo" {
   plan     = "lite"
   location = "us-south"
   name     = "terraform_demo"
   service  = "apprapp"
}
```
{: codeblock}

### `variables.tf`
{: #ac-variables-tf}

`variables.tf` stores passwords or other values that are required for Terraform at run time.

```hcl
variable "collection_name" {
	type        = string
	default     = "terraform_collection"
	description = "Collection name"
}

variable "collection_id" {
	type        = string
	default     = "collection123"
	description = "Collection ID"
}

variable "environment_id" {
	type        = string
	default     = "dev"
	description = "Environment ID"
}

variable "featureFlag_name" {
	type        = string
	default     = "terraform_featureFlag"
	description = "Feature flag name"
}

variable "featureFlag_type" {
	type        = string
	default     = "BOOLEAN"
	description = "Feature flag type"
}

variable "featureFlag_id" {
	type        = string
	default     = "featureFlag123"
	description = "Feature flag ID"
}

variable "featureFlag_enabled" {
	type        = string
	default     = "true"
	description = "Feature flag enabled value"
}

variable "featureFlag_disabled" {
	type        = string
	default     = "false"
	description = "Feature flag disabled value"
}

variable "featureFlag_rollout" {
	type        = string
	default     = "50"
	description = "Feature flag rollout percentage value"
}

variable "segment_name" {
	type        = string
	default     = "terraform_segment"
	description = "Segment name"
}

variable "segment_id" {
	type        = string
	default     = "s6"
	description = "Segment ID"
}

variable "segment_description" {
	type        = string
	default     = "testing segment create"
	description = "Description for the segment"
}

variable "attribute_values" {
	type        = list(any)
	default     = ["India", "UK"]
	description = "Values for segment attribute"
}
```
{: codeblock}

### `collections.tf`
{: #ac-collections-tf}

`collections.tf` uses {{site.data.keyword.appconfig_short}} to create collections.

```hcl
resource "ibm_app_config_collection" "app_config_collection" {
  guid          = ibm_resource_instance.terraform_demo.guid
  name          = var.collection_name
  description   = "Description for the collection"
  collection_id = var.collection_id
}
```
{: codeblock}

### `featureFlags.tf`
{: #ac-featureFlags-tf}

`featureFlags.tf` uses {{site.data.keyword.appconfig_short}} to create feature flag.

```hcl
resource "ibm_app_config_feature" "app_config_feature" {
  guid               = ibm_resource_instance.terraform_demo.guid
  name               = var.featureFlag_name
  type               = var.featureFlag_type
  feature_id         = var.featureFlag_id
  enabled_value      = var.featureFlag_enabled
  environment_id     = var.environment_id
  disabled_value     = var.featureFlag_disabled
  rollout_percentage = var.featureFlag_rollout
}
```
{: codeblock}


### `segments.tf`
{: #ac-segments-tf}

`segments.tf` uses {{site.data.keyword.appconfig_short}} to create segments.

```hcl
resource "ibm_app_config_segment" "app_config_create_segment" {
 guid            = ibm_resource_instance.terraform_demo.guid
 name            = var.segment_name
 description     = var.segment_description
 tags            = "t1"
 segment_id      = var.segment_id
 rules {
  attribute_name = "country"
  operator       = "contains"
  values         = var.attribute_values
 }
}
```
{: codeblock}

## Running your Terraform
{: #ac-execute-tf}
{: step}

Before running any Terraform scripts, learn about the following Terraform commands:

### Terraform **init**
{: #ac-init-tf}

The Terraform **init** command prepares the environment by ensuring the directory is properly configured:

```bash
bash-5.1# terraform init

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of ibm-cloud/ibm from the dependency lock file
- Using previously-installed ibm-cloud/ibm v1.56.0

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```
{: codeblock}

### Terraform **plan**
{: #ac-plan-tf}

The Terraform **plan** command compares the declared resources with the state file to print the resources to be created, altered, or destroyed. This step shows you the impact of the resource files.

```bash
bash-5.1# terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # ibm_app_config_collection.app_config_collection will be created
  + resource "ibm_app_config_collection" "app_config_collection" {
      + collection_id    = "collection123"
      + created_time     = (known after apply)
      + description      = "Description for the collection"
      + features_count   = (known after apply)
      + guid             = (known after apply)
      + href             = (known after apply)
      + id               = (known after apply)
      + name             = "terraform_collection"
      + properties_count = (known after apply)
      + updated_time     = (known after apply)
    }

  # ibm_app_config_feature.app_config_feature will be created
  + resource "ibm_app_config_feature" "app_config_feature" {
      + created_time       = (known after apply)
      + disabled_value     = "false"
      + enabled            = (known after apply)
      + enabled_value      = "true"
      + environment_id     = "dev"
      + feature_id         = "featureFlag123"
      + guid               = (known after apply)
      + href               = (known after apply)
      + id                 = (known after apply)
      + name               = "terraform_featureFlag"
      + rollout_percentage = 50
      + segment_exists     = (known after apply)
      + type               = "BOOLEAN"
      + updated_time       = (known after apply)
    }

  # ibm_app_config_segment.app_config_create_segment will be created
  + resource "ibm_app_config_segment" "app_config_create_segment" {
      + created_time = (known after apply)
      + description  = "testing segment create"
      + guid         = (known after apply)
      + href         = (known after apply)
      + id           = (known after apply)
      + name         = "terraform_segment"
      + segment_id   = "s6"
      + tags         = "testing"
      + updated_time = (known after apply)

      + rules {
          + attribute_name = "country"
          + operator       = "contains"
          + values         = [
              + "India",
              + "UK",
            ]
        }
    }

  # ibm_resource_instance.terraform_demo will be created
  + resource "ibm_resource_instance" "terraform_demo" {
      + account_id              = (known after apply)
      + allow_cleanup           = (known after apply)
      + created_at              = (known after apply)
      + created_by              = (known after apply)
      + crn                     = (known after apply)
      + dashboard_url           = (known after apply)
      + deleted_at              = (known after apply)
      + deleted_by              = (known after apply)
      + extensions              = (known after apply)
      + guid                    = (known after apply)
      + id                      = (known after apply)
      + last_operation          = (known after apply)
      + location                = "us-south"
      + locked                  = (known after apply)
      + name                    = "terraform_demo"
      + plan                    = "lite"
      + plan_history            = (known after apply)
      + resource_aliases_url    = (known after apply)
      + resource_bindings_url   = (known after apply)
      + resource_controller_url = (known after apply)
      + resource_crn            = (known after apply)
      + resource_group_crn      = (known after apply)
      + resource_group_id       = (known after apply)
      + resource_group_name     = (known after apply)
      + resource_id             = (known after apply)
      + resource_keys_url       = (known after apply)
      + resource_name           = (known after apply)
      + resource_plan_id        = (known after apply)
      + resource_status         = (known after apply)
      + restored_at             = (known after apply)
      + restored_by             = (known after apply)
      + scheduled_reclaim_at    = (known after apply)
      + scheduled_reclaim_by    = (known after apply)
      + service                 = "apprapp"
      + service_endpoints       = (known after apply)
      + state                   = (known after apply)
      + status                  = (known after apply)
      + sub_type                = (known after apply)
      + tags                    = [
          + "terraform-learning-19aug",
        ]
      + target_crn              = (known after apply)
      + type                    = (known after apply)
      + update_at               = (known after apply)
      + update_by               = (known after apply)
    }

Plan: 4 to add, 0 to change, 0 to destroy.

```
{: codeblock}

## Exporting an API key
{: #ac-exportkey-tf}
{: step}

Export your {{site.data.keyword.cloud_notm}} API Key before running the **apply** command:

```bash
export IBMCLOUD_API_KEY={Your IBM Cloud API Key}
```
{: codeblock}

## Running Terraform **apply**
{: #ac-apply-tf}
{: step}

The Terraform **apply** command implements the changes that are declared during the **plan** step and deploys the resource to the {{site.data.keyword.cloud_notm}}.

```bash
bash-5.1# terraform apply

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # ibm_app_config_collection.app_config_collection will be created
  + resource "ibm_app_config_collection" "app_config_collection" {
      + collection_id    = "collection123"
      + created_time     = (known after apply)
      + description      = "Description for the collection"
      + features_count   = (known after apply)
      + guid             = (known after apply)
      + href             = (known after apply)
      + id               = (known after apply)
      + name             = "terraform_collection"
      + properties_count = (known after apply)
      + updated_time     = (known after apply)
    }

  # ibm_app_config_feature.app_config_feature will be created
  + resource "ibm_app_config_feature" "app_config_feature" {
      + created_time       = (known after apply)
      + disabled_value     = "false"
      + enabled            = (known after apply)
      + enabled_value      = "true"
      + environment_id     = "dev"
      + feature_id         = "featureFlag123"
      + guid               = (known after apply)
      + href               = (known after apply)
      + id                 = (known after apply)
      + name               = "terraform_featureFlag"
      + rollout_percentage = 50
      + segment_exists     = (known after apply)
      + type               = "BOOLEAN"
      + updated_time       = (known after apply)
    }

  # ibm_app_config_segment.app_config_create_segment will be created
  + resource "ibm_app_config_segment" "app_config_create_segment" {
      + created_time = (known after apply)
      + description  = "testing segment create"
      + guid         = (known after apply)
      + href         = (known after apply)
      + id           = (known after apply)
      + name         = "terraform_segment"
      + segment_id   = "s6"
      + tags         = "testing"
      + updated_time = (known after apply)

      + rules {
          + attribute_name = "country"
          + operator       = "contains"
          + values         = [
              + "India",
              + "UK",
            ]
        }
    }

  # ibm_resource_instance.terraform_demo will be created
  + resource "ibm_resource_instance" "terraform_demo" {
      + account_id              = (known after apply)
      + allow_cleanup           = (known after apply)
      + created_at              = (known after apply)
      + created_by              = (known after apply)
      + crn                     = (known after apply)
      + dashboard_url           = (known after apply)
      + deleted_at              = (known after apply)
      + deleted_by              = (known after apply)
      + extensions              = (known after apply)
      + guid                    = (known after apply)
      + id                      = (known after apply)
      + last_operation          = (known after apply)
      + location                = "us-south"
      + locked                  = (known after apply)
      + name                    = "terraform_demo"
      + plan                    = "lite"
      + plan_history            = (known after apply)
      + resource_aliases_url    = (known after apply)
      + resource_bindings_url   = (known after apply)
      + resource_controller_url = (known after apply)
      + resource_crn            = (known after apply)
      + resource_group_crn      = (known after apply)
      + resource_group_id       = (known after apply)
      + resource_group_name     = (known after apply)
      + resource_id             = (known after apply)
      + resource_keys_url       = (known after apply)
      + resource_name           = (known after apply)
      + resource_plan_id        = (known after apply)
      + resource_status         = (known after apply)
      + restored_at             = (known after apply)
      + restored_by             = (known after apply)
      + scheduled_reclaim_at    = (known after apply)
      + scheduled_reclaim_by    = (known after apply)
      + service                 = "apprapp"
      + service_endpoints       = (known after apply)
      + state                   = (known after apply)
      + status                  = (known after apply)
      + sub_type                = (known after apply)
      + tags                    = [
          + "terraform-learning-19aug",
        ]
      + target_crn              = (known after apply)
      + type                    = (known after apply)
      + update_at               = (known after apply)
      + update_by               = (known after apply)
    }

Plan: 4 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

ibm_resource_instance.terraform_demo: Creating...
ibm_resource_instance.terraform_demo: Still creating... [10s elapsed]
ibm_resource_instance.terraform_demo: Still creating... [20s elapsed]
ibm_resource_instance.terraform_demo: Still creating... [30s elapsed]
ibm_resource_instance.terraform_demo: Creation complete after 31s
ibm_app_config_collection.app_config_collection: Creating...
ibm_app_config_segment.app_config_create_segment: Creating...
ibm_app_config_feature.app_config_feature: Creating...
ibm_app_config_collection.app_config_collection: Creation complete after 2s
ibm_app_config_segment.app_config_create_segment: Creation complete after 2s
ibm_app_config_feature.app_config_feature: Creation complete after 2s

Apply complete! Resources: 4 added, 0 changed, 0 destroyed.

```
{: codeblock}

## Validating resources
{: #ac-validate-tf}
{: step}

Validate resources within the {{site.data.keyword.cloud_notm}} by selecting the resource list in [resources](https://cloud.ibm.com/resources){: external}.

For more information on API and SDK references, tutorials, and FAQs, for {{site.data.keyword.cloud_notm}} products and services, see [Documentation](https://cloud.ibm.com/docs).
