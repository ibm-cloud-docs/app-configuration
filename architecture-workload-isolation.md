---

copyright:
  years: 2020, 2024
lastupdated: "2024-03-25"

keywords: public isolation for app configuration, compute isolation for app configuration, app configuration architecture, workload isolation in app configuration

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Learning about {{site.data.keyword.appconfig_short}} architecture and workload isolation
{: #compute-isolation}

Learn about the {{site.data.keyword.appconfig_full}} service architecture, the service dependencies, and how customer workloads are isolated from each other in {{site.data.keyword.appconfig_short}} instances.
{: shortdesc}

## {{site.data.keyword.appconfig_short}} architecture
{: #architecture}

{{site.data.keyword.appconfig_notm}} service is offered in the regions: Dallas, Washington DC, London, Frankfurt and Sydney. Every region supported, has its own {{site.data.keyword.cloud_notm}} Kubernetes Service cluster with several worker nodes. Each worker node runs several instances of {{site.data.keyword.appconfig_short}} service components. Each region is fronted by a global load balancer and a web application firewall.

{{site.data.keyword.appconfig_short}} service persists tenant data in highly available database. A single regional database is used to store the data of all tenants in that particular region.

The data is stored across multiple zones in each region for high availability. Data that is stored is encrypted and persisted in a database cluster that is spread across availability zones. All databases connections use TLS/SSL encryption for data in transit.

![Architecture](images/arch.png "Architecture diagram"){: caption="Figure 1. {{site.data.keyword.appconfig_notm}} architecture" caption-side="bottom"}

The Feature server component provides the API interface to the {{site.data.keyword.appconfig_short}} service.

The data store component stores all configuration, metrics, instance details, and environments data.

The {{site.data.keyword.appconfig_short}} UI is the front-end component, which can be used to manage the configuration data.

Analytics server component collects the usage metrics for configuration data and stores it to the data store at instance level.

## {{site.data.keyword.appconfig_short}} workload isolation
{: #workload-isolation}

Each regional deployment of the {{site.data.keyword.appconfig_full}} serves multiple tenants that are identified by the {{site.data.keyword.IBM_notm}} service instance.

- The {{site.data.keyword.appconfig_notm}} service in a region is a multi-tenant highly available service.
- The configuration data that is collected and processed by the {{site.data.keyword.appconfig_notm}} service is associated with the service instance that is created by a tenant. This configuration data is not visible to the other service instances by virtue of this association.
- Data for all tenants is colocated in the same data store and segmented by the tenant-specific instance `guid`. Retrieval of tenant-specific data is enforced by access control policies.
