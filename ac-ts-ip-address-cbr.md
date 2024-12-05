---

copyright:
  years: 2023, 2024
lastupdated: "2024-10-07"

keywords: app-configuration, app configuration, troubleshooting, faqs, Frequently Asked Questions, question, can't create IAM credentials, can't regenerate IAM credentials, IAM credentials not working, IP address restrictions enabled, IP address not allowed

subcollection: app-configuration

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I get the "You do not have permission to perform this action." message when trying to use the {{site.data.keyword.appconfig_short}} service instance?
{: #ac-ip-address-not-allowed}
{: troubleshoot}
{: support}

When you try to use {{site.data.keyword.appconfig_short}} service instance you are unable to perform any action.
{: shortdesc}

When you try to access any feature in {{site.data.keyword.appconfig_short}} service instance either through the console or API or CLI, you may encounter an error similar to any of the following examples:
{: tsSymptoms}

```json
You do not have permission to perform this action. Contact your service Administrator.
```
{: screen}

or

```json
{
  "message": "Unauthorized"
}
```

This is due to the reason that you are trying to access the {{site.data.keyword.appconfig_short}} service instance from a Network Zone which is outside of the defined Network zone in your account's Context-based restrictions settings.
{: tsCauses}

To resolve the issue, make sure that your Context-based restrictions settings in the account are updated to allow the IP addresses that correspond with your network in the Network Zone's Allowed IP addresses.
{: tsResolve}

As an administrator of your {{site.data.keyword.appconfig_short}} service instance perform the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage > Context-based restrictions**.
1. Go to **Network zones** and then select the required Network Zone and select **Edit** from the overflow menu.
1. In the **Allowed IP addresses**, include the required IP addresses that you want to enable access to the {{site.data.keyword.appconfig_short}} service instance.
1. Click **Update**.

For more information, see [Managing access with context-based restrictions](/docs/app-configuration?topic=app-configuration-ac-restrict-access-cbr).
