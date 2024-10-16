---

copyright:
  years: 2019, 2023
lastupdated: "2023-04-10"

keywords: app-configuration activity tracker events, app configuration events, app configuration audit, app configuration audit events, app configuration audit logs

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Auditing events
{: #ac-at_events}

Security officers, auditors, or managers can use the {{site.data.keyword.at_full_notm}} service to track how users and applications interact with the {{site.data.keyword.appconfig_short}} service in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see the [getting started tutorial for {{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started).

## List of events
{: #ac-events}

The following list of {{site.data.keyword.appconfig_short}} events is sent to {{site.data.keyword.at_full_notm}}.
{: shortdesc}

| Action             | Description      |
| -------------------| -----------------|
| `apprapp.segments.create` | Created a segment or failed to create |
| `apprapp.segments.update` | Updated a segment or failed to update |
| `apprapp.segments.delete` | Deleted a segment or failed to delete |
| `apprapp.segments.list` | Called the list of segments or failed to list |
| `apprapp.segments.read` | Retrieved segment details or failed to retrieve |
| `apprapp.environments.create` | Created an environment or failed to create |
| `apprapp.environments.update` | Updated an environment or failed to update |
| `apprapp.environments.delete` | Deleted an environment or failed to delete |
| `apprapp.environments.list` | Called the list of environments or failed to list |
| `apprapp.environments.read`| Retrieved environment details or failed to retrieve environment details |
| `apprapp.features.create`| Created feature or failed to create |
| `apprapp.features.update` | Updated feature or failed to update |
| `apprapp.features.updatevalues` | Updated feature details or failed to update details |
| `apprapp.features.delete` | Deleted feature or failed to delete |
| `apprapp.features.list` | Called the list of features or failed to list |
| `apprapp.features.read` | Retrieved feature details or failed to retrieve the details |
| `apprapp.features.evaluate` | Evaluated feature at the SDK or failed to evaluate |
| `apprapp.features.toggle` | Toggled feature or failed to toggle |
| `apprapp.properties.create` | Created a property or failed to create |
| `apprapp.properties.update` | Updated property or failed to update |
| `apprapp.properties.updatevalues`| Updated property details or failed to update |
| `apprapp.properties.delete` | Deleted property or failed to delete |
| `apprapp.properties.list` | Called the list of properties or failed to list |
| `apprapp.properties.read` | Retrieved details of property or failed to retrieve property details |
| `apprapp.properties.evaluate` | Evaluated property at the SDK or failed to evaluate |
| `apprapp.collections.create` | Created a collection or failed to create |
| `apprapp.collections.update` | Updated a collection or failed to update |
| `apprapp.collections.delete` | Deleted a collection or failed to update |
| `apprapp.collections.list` | Called the list of collections or failed to list |
| `apprapp.collections.read` | Retrieved collection details or failed to retrieve collection details |
| `apprapp.snapshots.create` | Created a snapshot configuration or failed to create |
| `apprapp.snapshots.update` | Updated a snapshot configuration or failed to update |
| `apprapp.snapshots.delete` | Deleted a snapshot configuration or failed to delete |
| `apprapp.snapshots.list` | Called the list of snapshot configuration or failed to list |
| `apprapp.snapshots.read` | Retrieved snapshot configuration details or failed to retrieve snapshot configuration details |
| `apprapp.snapshots.promote` | Created or updated the chosen configuration to GitHub based on the snapshots configuration. |
| `apprapp.snapshots.restore` | Writes or updates the chosen snapshot configuration from the GitHub to {{site.data.keyword.appconfig_short}} instance. |
| `apprapp.originconfigs.update` | Updated the allowlist of origins or failed to update |
| `apprapp.originconfigs.list` | Called the allowlist of origins or failed to list |
| `apprapp.workflowconfigs.list` | Get the workflow configurations or failed to list |
| `apprapp.workflowconfigs.create` | Create a workflow configuration or failed to create  |
| `apprapp.workflowconfigs.update` | Update a workflow configuration or failed to update |
| `apprapp.workflowconfigs.delete` | Delete a workflow configuration or failed to delete |
| `apprapp.changerequest.create` | Creates the Change Request for workflow integration or failed to create |
| `apprapp.changerequest.update` | Captures the change of events in the Change Request of Service Now for workflow or failed to update |
| `apprapp.config.import` | Import a instance configuration. |
| `apprapp.config.export` | Export instance configuration. |
| `apprapp.config.action` | Promotes or Restores a Snapshot configuration to or from GitHub respectively. |
| `apprapp.configaggregatorsettings.update` | Updates the configuration aggregator recording set-up and allows to either enable or disable the feature or failed to update |
| `apprapp.configaggregatorsettings.list` | Called to view the settings configuration or failed to list |
| `apprapp.configaggregatorstatus.list` | Called to view status and time when the last configuration got updated or failed to list. |
| `apprapp.configaggregator.query` | Called to list the resource configurations. |
{: caption="Overview of {{site.data.keyword.appconfig_short}} actions that generate {{site.data.keyword.at_full_notm}} events" caption-side="bottom"}

If an unauthorized request is made for any of the actions in table 1, a management event with reason code 403 is emitted.
{: note}

## Viewing events
{: #at_ui}

Events that are generated by {{site.data.keyword.appconfig_short}} are automatically forwarded to the {{site.data.keyword.at_full_notm}} service instance available in the same location.

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_full_notm}} service in the same location where your service instance is available.

1. Create a service instance of [{{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started).

1. [Start the {{site.data.keyword.at_full_notm}} web console](/docs/activity-tracker?topic=activity-tracker-launch) to access your events.
