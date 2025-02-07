---

copyright:
  years: 2021, 2025
lastupdated: "2025-02-07"

keywords: app-configuration, app configuration, securing your data

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Securing your data in {{site.data.keyword.appconfig_short}}
{: #ac-securing-your-data}

To ensure that you can securely manage your data when you use {{site.data.keyword.appconfig_short}}, it is important to know exactly what data is stored and encrypted. It is also important to know how you can delete any stored data.
{: shortdesc}

## What information is stored in {{site.data.keyword.appconfig_short}}?
{: #ac-information-stored}

The following information are stored when you use {{site.data.keyword.appconfig_short}} service dashboard or API or CLI:

- Instance details
- Environments
- Collections
- Properties
- Features
- Segment rules

These information can be deleted using the APIs mentioned [here](https://cloud.ibm.com/apidocs/app-configuration){: external}. Deletion of information is deleted permanently from the service.

## How your data is stored and encrypted in {{site.data.keyword.appconfig_short}}
{: #ac-data-store-encryption}

{{site.data.keyword.appconfig_short}} stores and encrypts definitions of environments, collections, features, properties and segment rules. This data is encrypted at rest.  As a multi-tenant service, any data stored is encrypted with the default IBM provided key for all tenants.

IBM personnel have access to the configuration data. It is recommended to avoid storing sensitive information as part of the configuration. If sensitive data storage is required, consider using [IBM Cloud Secrets Manager](https://cloud.ibm.com/docs/secrets-manager?topic=secrets-manager-getting-started){: external}.

You can add a higher level of encryption control to your data at rest (when it is stored) by enabling integration with a Key Management Service (KMS). The data that you store in {{site.data.keyword.cloud_notm}} is encrypted at rest by using envelope encryption. If you need to control the encryption keys, you can integrate Key Protect or Hyper Protect Crypto Services. This process is commonly referred to as Bring Your Own Key (BYOK). With Key Protect and Hyper Protect Crypto Services, you can create, import, and manage encryption keys. You can assign access policies to the keys, assign users or service IDs to the keys, or give the key access only to a specific service.

For more information, see [Managing encryption](/docs/app-configuration?topic=app-configuration-ac-managing-encryption).

## How can I delete my information?
{: #ac-data-deletion}

When you delete an instance of {{site.data.keyword.appconfig_short}}, all of the associated data is also deleted. When the service instance is deleted, a 7-day reclamation period begins. During that time, you are able to restore the instance and all of the associated user data. However, if the instance and data are permanently deleted, it cannot be restored. {{site.data.keyword.appconfig_short}} does not store any data from permanently deleted instances.

The {{site.data.keyword.appconfig_short}} data retention policy describes how long your data is stored after you delete the service. The data retention policy is included in the {{site.data.keyword.appconfig_short}} service description, which you can find in the [IBM Cloud Terms and Notices](https://cloud.ibm.com/docs/overview?topic=overview-terms){: external}.

### Deleting an instance
{: #ac-deleting-instance}

If you no longer need an instance of {{site.data.keyword.appconfig_short}}, you can delete the service instance and any data that is stored using `ibmcloud CLI`. You can also choose to delete your service instance by using the console.

To restore a deleted instance or to delete the instance permanently you can use Resource Reclamations. Refer to [Using resource reclamations](https://cloud.ibm.com/docs/account?topic=account-resource-reclamation){: external} to know more on the resource reclamation.
