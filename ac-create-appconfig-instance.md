---

copyright:
  years: 2020
lastupdated: "2020-11-10"

keywords: app-configuration, app configuration, create an instance

subcollection: app-configuration

---

{:codeblock: .codeblock}
{:external: target="_blank" .external}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Create an {{site.data.keyword.appconfig_notm}} service instance
{: #ac-create-an-instance}

{{site.data.keyword.appconfig_notm}} provides capabilities to embark on a truly agile development methodology by separating feature rollouts from regular release cycles. Reduce risk by controlling the release of features and rolling back as required. Create user segments and target features to selected user segments based on different criteria.
{: shortdesc}

You need an {{site.data.keyword.cloud}} account to create an instance of the {{site.data.keyword.appconfig_short}} service.
{: note}

To create an {{site.data.keyword.appconfig_short}} service instance, follow these steps.

1. Log in to your {{site.data.keyword.cloud_notm}} account.
1. In the [IBM Cloud catalog](https://cloud.ibm.com/catalog#services), search **App Configuration** and select [App Configuration](https://cloud.ibm.com/catalog/services/apprapp). The service configuration screen opens.

   ![Create an {{site.data.keyword.appconfig_short}} service instance](images/ac-create-instance.png "Creating an {{site.data.keyword.appconfig_short}} service instance"){: caption="Figure 1. {{site.data.keyword.appconfig_short}} service instance" caption-side="bottom"}

1. **Select a region** - Currently, Dallas (us-south) and London (eu-gb) region is supported.
1. **Select a pricing plan** - Currently, only Standard pricing plan is defined. The standard plan includes all the features that are enabled as on time. You can use simple and uniform ReST APIs to configure, enable, segment, and monitor features to mobile devices and web applications.
1. **Configure your resource** with a **Service name**, or use the preset name.
1. **Select a resource group** - The resource group selection helps how you want resources to be organized in your account. The resource group that you select cannot be changed after the service instance is created.
1. Optionally, define **Tags** that are required to identify this service instance. If your tags are billing related, consider writing tags as *key:value* pairs to help group-related tags, such as `costctr:124`.
1. Click **Create**. A new service instance is created and the {{site.data.keyword.appconfig_short}} console displayed.

   ![{{site.data.keyword.appconfig_short}} console](images/ac-console.png "{{site.data.keyword.appconfig_short}} console"){: caption="Figure 2. {{site.data.keyword.appconfig_short}} console" caption-side="bottom"}
