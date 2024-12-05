---

copyright:
  years: 2021, 2024
lastupdated: "2024-10-07"

keywords: HA for app-configuration, data model, high availability for app configuration, ha

subcollection: app-configuration
---

{{site.data.keyword.attribute-definition-list}}

# Understanding high availability for {{site.data.keyword.appconfig_short}}
{: #ac-ha}

{{site.data.keyword.IBM_notm}} {{site.data.keyword.appconfig_short}} is a highly available, multi-tenant, regional service.
{: shortdesc}

## Service High Availability (HA)
{: #ac-service-ha}

An availability zone is a logically and physically isolated location within an {{site.data.keyword.cloud_notm}} region where your data is processed and hosted.

- An availability zone has independent power, cooling, and network infrastructures that are isolated from other zones to strengthen fault tolerance by avoiding single points of failure between zones.
- An availability zone offers high bandwidth and low inter-zone latency within a region.

A region (location) is a geographically and physically separate group of one or more availability zones with independent electrical and network infrastructures that are isolated from other regions.

- Regions are designed to remove shared single points of failure with other regions and provide low inter-zone latency within the region.
- Each region has three different data centers (DC) for redundancy.
- In each supported region, traffic is load balanced across infrastructure in multiple availability zones, with no single point of failure.
- If all the data centers in a region fail, {{site.data.keyword.appconfig_short}} becomes unavailable in that region.

## Availability zones for {{site.data.keyword.appconfig_short}}
{: #ac-zones-ha}

The following table lists the high-availability (HA) status for the regions (locations) where the {{site.data.keyword.appconfig_notm}} service is available:

| Geography| Region| HA Status |
|----------|-------|-----------|
| Asia-Pacific| Sydney (au-syd)|MZR|
| Europe | London (eu-gb)|MZR|
| Europe | Frankfurt (eu-de)|MZR|
| North America| Dallas (us-south)|MZR|
| North America| Washington DC (us-east)|MZR|
{: caption="HA status for the regions" caption-side="bottom"}

Where:

- A *geography* is a geographic area or larger political body that contains one or more regions.
- A *region* is a defined geographic territory.
   - A region might be a specific postal code area, a town, a city, a state, a group of states, or even a group of countries.
   - A region contains [multiple availability zones](https://www.ibm.com/cloud/data-centers/) to meet local access, low latency, and security requirements for the region.
- `MZR` means multi-zone region. [Learn more](/docs/overview?topic=overview-locations#table-mzr).

## Disaster recovery (DR) for {{site.data.keyword.appconfig_short}} service in a region
{: #ac-dr}

App Configuration is a regional service, and does not offer automatic cross-regional failover or cross-regional disaster recovery. If all of the availability zones in a region fail, App Configuration becomes unavailable in that region.
{: important}

If an entire MZR becomes inoperative (usually due to a catastrophic disaster or failure), {{site.data.keyword.IBM_notm}} runs disaster-recovery plans to restore service within 24 hours or less. {{site.data.keyword.IBM_notm}} restores the service in an alternative MZR from an IBM-managed backup. Existing DNS names are migrated to the backup deployment. When the disaster recovery process is complete, API traffic resumes automatically.

When the primary MZR is restored, the secondary deployment is migrated back to the primary site. After the migration is complete, the DNS is restored to its original routing.

If you need zero downtime during a regional disaster recovery, create and maintain backup instances in other regions. To synchronize a service instance in one region with an instance in a different region, you can use the APIs mentioned [here](/apidocs/app-configuration).
