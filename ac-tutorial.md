---

copyright:
  years: 2020, 2025
lastupdated: "2025-06-12"

keywords: app-configuration, app configuration, tutorial

subcollection: app-configuration

content-type: tutorial
account-plan: standard
completion-time: 90m

---

{{site.data.keyword.attribute-definition-list}}

# Working with {{site.data.keyword.appconfig_short}}
{: #ac-appconfig}
{: toc-content-type="tutorial"}
{: toc-services=""}
{: toc-completion-time="90m"}

{{site.data.keyword.appconfig_short}} enables app developers to quickly build mobile and web apps. With feature management of {{site.data.keyword.appconfig_short}}, you can embark on a truly agile development methodology by separating feature roll outs from release cycles. Reduce risk by controlling the release of features and rolling back as needed. Create user groups (segments) and target features to selected user groups based on different criteria.
{: shortdesc}

## Before you begin
{: #ac-prerequisite}

You need an {{site.data.keyword.cloud}} account. If you don't have an account, [create one](https://cloud.ibm.com/registration/){: external}. Log in to your {{site.data.keyword.cloud}} account.

## Create an {{site.data.keyword.appconfig_short}} service instance
{: #ac-create-an-apprapp-instance}
{: step}

The {{site.data.keyword.appconfig_short}} service provides a unified application development capability. Using these capabilities, you can quickly build mobile and web apps and roll out to targeted audience.

To create an {{site.data.keyword.appconfig_short}} service instance, see [Create an App Configuration service instance](/docs/app-configuration?topic=app-configuration-ac-create-an-instance).

## Create collections
{: #ac-create-collections}
{: step}

You can create a collection and enable App Service capabilities like feature flags and segmentation.

To create a collection, see [Create a collection](/docs/app-configuration?topic=app-configuration-ac-collections#ac-create-a-collection).

## Create Environment, Feature flags, and Properties
{: #ac-create-feature-flags}
{: step}

Create and manage environments, feature flags, and properties for collections across platforms. Using Feature flags you, as an app owner, can control the applicability of a feature by enabling or disabling it at run time. You can also manage the properties for distributed applications centrally.

- To create an environment, see [Create an environment](/docs/app-configuration?topic=app-configuration-ac-environments#ac-create-environment).
- To create a feature flag, see [Create a feature flag](/docs/app-configuration?topic=app-configuration-ac-feature-flags#ac-create-feature-flag).
- To create a property, see [Create a property](/docs/app-configuration?topic=app-configuration-ac-properties#ac-create-properties).

## Integrate {{site.data.keyword.appconfig_short}} service SDK
{: #ac-integrate-sdk}
{: step}

{{site.data.keyword.appconfig_short}} provides SDKs to integrate with your application. For more information about SDK installation and technical concepts, see [Integrating SDKs](/docs/app-configuration?topic=app-configuration-ac-sdks).

## Create segments
{: #ac-create-segments}
{: step}

Segments helps you to quickly turn features on or off for selective audience. Use segments to target feature flags for A/B testing and beta launches.

To create a segment, see [Create a segment](/docs/app-configuration?topic=app-configuration-ac-segments#ac-create-segment)

## Next steps
{: #ac-gs-next-steps}

- [How to target Feature flags to Segments](/docs/app-configuration?topic=app-configuration-ac-feature-flags#targeting-segment-with-feature-flag)
- [How to target Properties to Segments](/docs/app-configuration?topic=app-configuration-ac-properties#targeting-segment-with-properties)
- [Enable feature flag](/docs/app-configuration?topic=app-configuration-ac-feature-flags#enabling-feature-flag) (ON/OFF).
