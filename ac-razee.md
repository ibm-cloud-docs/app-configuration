---

copyright:
  years: 2021, 2022
lastupdated: "2022-07-14"

keywords: app-configuration, app configuration, razee plugin, razee

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Release your features across clusters with {{site.data.keyword.appconfig_short}}
{: #ac-razee-plugin}

[Razee](https://razee.io/) is an open source project that is developed by IBM to automate and manage the deployment of Kubernetes resources across clusters, environments, and cloud providers.
{: shortdesc}

{{site.data.keyword.appconfig_short}} uses Razee to release features across clusters and helps in templatizing the cluster resources. {{site.data.keyword.appconfig_short}} Razee plug-in helps in the following areas: 

- Custom resource development by using Razee
- Fetches the feature flag values from {{site.data.keyword.appconfig_short}} service instance 
- Templatizes and controls the deployment of Kubernetes resources across clusters

You can try the {{site.data.keyword.appconfig_short}} Razee plug-in from [here](https://github.com/IBM/appconfiguration-razee). 

## Common use cases for {{site.data.keyword.appconfig_short}} Razee plug-in 
{: #ac-usecases-razee-plugin}

- Controlling Kubernetes deployments to scale up or down for a segment of clusters 
- For few privileged customers, roll-out a new feature to their clusters, without any code deployments 
