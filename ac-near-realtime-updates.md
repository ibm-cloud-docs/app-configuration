---

copyright:
  years: 2020, 2026
lastupdated: "2026-09-28"

keywords: app-configuration, app configuration, configuration aggregator, real-time, activity tracker, event routing

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Enabling real-time configuration collection
{: #ac-near-realtime-updates}

Real-time resource configuration collection is a capability of Configuration Aggregator that supplements scheduled reconciliation by reacting to changes as they happen. Instead of waiting for the next periodic reconciliation cycle, Configuration Aggregator listens for configuration change events published by IBM Cloud services through Activity Tracker Event Routing. When a resource is created, modified, or deleted, the relevant event is forwarded to your {{site.data.keyword.appconfig_short}} instance and the affected resource record is updated within a few minutes.
{: shortdesc}

Real-time resource collection is available only on the Standard and Enterprise plans.
{: note}

## Benefits of real-time configuration collection
{: #ac-realtime-benefits}

- **Faster detection** - Configuration changes are detected within a few minutes instead of waiting for the next scheduled reconciliation.
- **Improved compliance** - Security and compliance issues can be identified and remediated more quickly.
- **Reduced latency** - Configuration data remains current with minimal delay.
- **Targeted updates** - Only affected resources are updated, reducing processing overhead.

## Before you begin
{: #ac-near-realtime-prerequisites}

- Ensure you have an {{site.data.keyword.appconfig_short}} instance on the Standard or Enterprise plan with Configuration Aggregator enabled. See [Configuration Aggregator](/docs/app-configuration?topic=app-configuration-ac-configuration-aggregator).

## Enabling real-time configuration collection
{: #ac-setup-activity-tracker-integration}

To enable real-time configuration collection, complete the following steps:

1. Create a service-to-service authorization policy:
   1. Go to **Manage** > **Access (IAM)** > **Authorizations**.
   2. Click **Create**.
   3. Select **Activity Tracker Event Routing** as the source service.
   4. Select **App Configuration** as the target service.
   5. Assign the **Configuration Update Reporter** role.

2. Configure Activity Tracker Event Routing to send events to your {{site.data.keyword.appconfig_short}} instance by creating an App Configuration target. Currently, only the CLI and API are supported for this step. For step-by-step instructions, see [Managing App Configuration targets (CLI)](/docs/atracker?topic=atracker-target_v2_appconf&interface=cli) or [Managing App Configuration targets (API)](/docs/atracker?topic=atracker-target_v2_appconf&interface=api) in the Activity Tracker documentation. When creating the target, select the regions from which you want to collect configuration change events.

   For Enterprise accounts, to support real-time events for sub-accounts, you must also create the Activity Tracker target and route in each child account using the parent account's {{site.data.keyword.appconfig_short}} instance CRN.
   {: note}

3. Activity Tracker Event Routing automatically forwards configuration change events to {{site.data.keyword.appconfig_short}}, which processes them and updates the configuration database.

To collect real-time Activity Tracker events for {{site.data.keyword.cos_full_notm}} buckets, you must explicitly enable Activity Tracking for each bucket. For more information, see [Enabling bucket audit events](/docs/cloud-logs?topic=cloud-logs-cos#cos_bucket_audit_events).
{: note}
