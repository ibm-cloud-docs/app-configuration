---

copyright:
  years: 2020, 2026
lastupdated: "2026-09-01"

keywords: app-configuration, app configuration, configuration aggregator, near real-time, activity tracker, event routing, cspm, workload protection

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Near real-time configuration collection
{: #ac-near-realtime-updates}

Near real-time resource configuration collection is a capability of Configuration Aggregator that supplements scheduled reconciliation by reacting to changes as they happen. Instead of waiting for the next periodic reconciliation cycle, Configuration Aggregator listens for configuration change events published by IBM Cloud services through Activity Tracker Event Routing. When a resource is created, modified, or deleted, the relevant event is forwarded to your {{site.data.keyword.appconfig_short}} instance and the affected resource record is updated within minutes. This allows governance and compliance tooling to act on current configuration state rather than potentially stale data.
{: shortdesc}

Near real-time resource collection is available only on the Standard and Enterprise plans.
{: note}

## Prerequisites
{: #ac-near-realtime-prerequisites}

Before you can enable near real-time configuration collection, you must:

1. Have an {{site.data.keyword.appconfig_short}} instance with Configuration Aggregator enabled. See [Configuration Aggregator](/docs/app-configuration?topic=app-configuration-ac-configuration-aggregator).
2. Set up service-to-service (S2S) authorization between Activity Tracker Event Routing and {{site.data.keyword.appconfig_short}}.
3. Configure Activity Tracker Event Routing to route events to your {{site.data.keyword.appconfig_short}} instance using an App Configuration target.

## Setting up Activity Tracker integration
{: #ac-setup-activity-tracker-integration}

To enable near real-time configuration collection:

1. Create a service-to-service authorization policy:
   - Go to **Manage** > **Access (IAM)** > **Authorizations**.
   - Click **Create**.
   - Select **Activity Tracker Event Routing** as the source service.
   - Select **App Configuration** as the target service.
   - Assign the **Configuration Update Reporter** role.

2. Configure Activity Tracker Event Routing to send events to your {{site.data.keyword.appconfig_short}} instance by creating an App Configuration target. For step-by-step instructions, see [Managing App Configuration targets](/docs/atracker?topic=atracker-target_v2_appconf&interface=ui) in the Activity Tracker documentation.
   - Select the regions from which you want to collect configuration change events.

3. Activity Tracker Event Routing automatically forwards configuration change events to {{site.data.keyword.appconfig_short}}, which processes them and updates the configuration database.


## Benefits of near real-time configuration collection
{: #ac-near-realtime-benefits}

- **Faster detection** - Configuration changes are detected within a few minutes instead of waiting for the next scheduled reconciliation.
- **Improved compliance** - Security and compliance issues can be identified and remediated more quickly.
- **Reduced latency** - Configuration data remains current with minimal delay.
- **Targeted updates** - Only affected resources are updated, reducing processing overhead.

## Real-time CSPM with Security and Compliance Center Workload Protection
{: #ac-realtime-cspm-workload-protection}

Configuration Aggregator, combined with near real-time updates, powers real-time cloud security posture management (CSPM) when integrated with {{site.data.keyword.sysdigsecure_full_notm}} (SCC Workload Protection). Instead of relying solely on periodic scans, Workload Protection can consume up-to-date resource configuration data from {{site.data.keyword.appconfig_short}} to continuously evaluate your IBM Cloud environment against security and compliance policies.

When a resource configuration changes in your account, the event flows from Activity Tracker Event Routing into {{site.data.keyword.appconfig_short}}, which updates the resource record. Workload Protection then reads this updated configuration and re-evaluates the affected resource against your configured policies. This end-to-end pipeline enables near-instantaneous detection of policy violations and misconfigurations.

### Setting up real-time CSPM
{: #ac-realtime-cspm-setup}

To enable real-time CSPM with Workload Protection and {{site.data.keyword.appconfig_short}}:

1. Connect your {{site.data.keyword.appconfig_short}} instance to your SCC Workload Protection instance. When configuring IBM Cloud CSPM within Workload Protection, an instance of {{site.data.keyword.appconfig_short}} with aggregation enabled is automatically connected.

2. Enable near real-time configuration collection by completing the steps in [Setting up Activity Tracker integration](#ac-setup-activity-tracker-integration).

3. Configure {{site.data.keyword.en_full_notm}} to forward configuration change notifications from {{site.data.keyword.appconfig_short}} to Workload Protection:
   - Connect your {{site.data.keyword.appconfig_short}} instance to an {{site.data.keyword.en_short}} instance. See [Integrating with {{site.data.keyword.en_short}}](/docs/app-configuration?topic=app-configuration-ac-int-en).
   - In your {{site.data.keyword.en_short}} instance, create a subscription that routes {{site.data.keyword.appconfig_short}} configuration change events to a COS bucket.




For full instructions on setting up real-time CSPM within Workload Protection, see [Getting started with SCC Workload Protection](/docs/workload-protection?topic=workload-protection-getting-started).
