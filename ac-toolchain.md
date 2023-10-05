---

copyright:
  years: 2021, 2023
lastupdated: "2023-03-31"

keywords: app-configuration, app configuration, toolchain integration, toolchain, devops, continuous delivery, tekton, otc

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Toolchain Integration
{: #ac-toolchain-integration}

Adopt a DevOps approach in your feature releases by using {{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_short}} service and {{site.data.keyword.cloud_notm}} {{site.data.keyword.contdelivery_short}}. {{site.data.keyword.contdelivery_short}} includes toolchains that automate the building of your applications.
{: shortdesc}

{{site.data.keyword.appconfig_short}} toolchain is based on Tekton and is available as a template at [https://github.com/ibm-cloud-appconfiguration/appconfiguration-toolchain](https://github.com/ibm-cloud-appconfiguration/appconfiguration-toolchain){: external} for automating the deployment of your applications.

Make sure you allowlist the traffic from Pipeline & toolchain services.
{: note}

Integrate {{site.data.keyword.appconfig_short}} service to a [toolchain](/docs/ContinuousDelivery?topic=ContinuousDelivery-toolchains_getting_started&interface=ui){: external} and apply feature flags and properties from the service instance to the environment or trigger properties of the associated pipeline.

This feature supports centralized management of feature flags and properties directly from an {{site.data.keyword.appconfig_short}} service instance.

[Learn more about configuring {{site.data.keyword.appconfig_short}} tool integration](/docs/ContinuousDelivery?topic=ContinuousDelivery-app-configuration&interface=ui){: external}.
