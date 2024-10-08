---

copyright:
  years: 2020, 2024
lastupdated: "2024-08-13"

keywords: app-configuration, app configuration, about app configuration

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# What is {{site.data.keyword.appconfig_short}}?
{: #ac-about}

{{site.data.keyword.appconfig_notm}} is a centralized feature management and configuration service for use with web and mobile applications, microservices, and distributed environments.
{: shortdesc}

Instrument your applications with {{site.data.keyword.appconfig_short}} SDKs, and use the {{site.data.keyword.appconfig_short}} dashboard or {{site.data.keyword.appconfig_short}} administrator API to define features flags, which are organized into collections and targeted to segments. Change feature flag states in the cloud to activate or deactivate features in your application or environment, often without restarting. You can also manage the properties for distributed applications centrally. It can facilitate a Cloud Governance SME with up-to-date configuration data of IBM Cloud resources in one place so that comprehensive information is available for goverance and compliance initiatives. This can be controlled with the ability to enable or disable the congiguration aggregation.

- **App Owners** - Roll out features by segment and independent from code deployments.
- **Developers** - Reduce source code branch complexity and troublesome merges by including untested or unfinished features behind a feature flag in your main branch.
- **Testers** - Test new features in production and be assured of a smooth transition. Use flags to activate untested features only for testers and QA personnel until it's time to release.

## Features
{: #ac-features}

Key features of {{site.data.keyword.appconfig_short}}:

- **Centralized configuration** - Configure multiple, distributed resources from a central location. Use collections to organize your flags by app or resource.
- **Dark Launch** - Includes features that are not ready for launch into your deployments, and activate them when they are ready.
- **Segmented Feature Rollout** - Activate features for different segments at different times, or vary features by segment.
- **Feature Rollback** - Instantly roll back problematic features by toggling feature flags in the {{site.data.keyword.appconfig_short}} cloud dashboard.
- **Phased Rollout** - Configure feature flag to be enabled for a subset of entities to implement progressive delivery of features.
- **Configuration Aggregator** - Configure to collect the metadata of multiple, distributed resources in IBM Cloud accounts to make available for governance and compliance initiatives.
