---

copyright:
  years: 2022
lastupdated: "2022-10-20"

keywords: app-configuration, app configuration, integrations, key protect, key management, hyper protect, hpcs

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Integrations
{: #ac-integrations}

Integrations in {{site.data.keyword.appconfig_short}} represent list of other {{site.data.keyword.cloud_notm}} services that are connected to your {{site.data.keyword.appconfig_short}} instance. You can encrypt the data that you store in {{site.data.keyword.cloud_notm}} databases by using encryption keys that you can control.
{: shortdesc}

You can use either one of the following options:
- Bring Your Own Key (BYOK) through {{site.data.keyword.keymanagementservicelong_notm}}, and use one of your own keys to encrypt your databases and backups.
- Hyper Protect Crypto Services (HPCS) - {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, a dedicated key management service, and Hardware Security Module (HSM) that provides you with the Keep Your Own Key capability for cloud data encryption with exclusive control of your encryption keys.

BYOK and KYOK capabilities are supported only for {{site.data.keyword.appconfig_short}} Enterprise plan.
{: important}

## Integrating with {{site.data.keyword.keymanagementserviceshort}}
{: #ac-int-key-protect}

You can create and bring keys that are created by using {{site.data.keyword.keymanagementserviceshort}}. To get started, you need [{{site.data.keyword.keymanagementserviceshort}}](https://cloud.ibm.com/catalog/key-protect){: external} provisioned on your {{site.data.keyword.cloud_notm}} account. For more information, see [provisioning a key protect instance](https://cloud.ibm.com/docs/key-protect?topic=key-protect-provision){: external}.

1. From your {{site.data.keyword.appconfig_short}} service instance dashboard, click **Integrations**. By default, the integrations display the list of other {{site.data.keyword.cloud_notm}} services that are connected to your {{site.data.keyword.appconfig_short}} instance.

1. From the **Connect** drop-down list, select **Key management**. This displays the **Key Management** side panel.

1. Select **Key Protect** from the **Service** drop-down list.

1. For the **Instance**, select one of these options:
   - **Create a new instance** - to create a new **Key Protect** instance. This takes you to the [{{site.data.keyword.keymanagementserviceshort}}](https://cloud.ibm.com/catalog/key-protect){: external} provisioning page.
   - **Choose existing instance** - select this option if you already have a {{site.data.keyword.keymanagementserviceshort}} instance. Select the **Service** instance and **Root key** from the drop-down list.

1. Click **Update** to apply the use your {{site.data.keyword.keymanagementserviceshort}} instance's root key to encrypt the data stored by your {{site.data.keyword.appconfig_short}} instance.

The newly created **Key management** information is listed in the **Integrations** dashboard.

The overflow menu consists of:
- `Disconnect` - helps you to disconnect the root key that is used for encrypting the data that is stored by your {{site.data.keyword.appconfig_short}} instance.
- `Delete` - helps you to delete the entry from the list, when a {{site.data.keyword.keymanagementserviceshort}} instance is deleted.

