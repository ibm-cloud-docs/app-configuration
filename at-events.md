---

copyright:
  years: 2018, 2025
lastupdated: "2025-04-01"

keywords: activity tracking, app-configuration cloud logs events, app configuration events, app configuration audit, app configuration audit events, app configuration audit logs

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Activity tracking events for {{site.data.keyword.appconfig_short}}
{: #at_events}


{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.appconfig_short}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.



As of 28 March 2024, the {{site.data.keyword.at_full_notm}} service is deprecated and will no longer be supported as of 30 March 2025. Customers will need to migrate to {{site.data.keyword.logs_full_notm}} before 30 March 2025. During the migration period, customers can use {{site.data.keyword.at_full_notm}} along with {{site.data.keyword.logs_full_notm}}. Activity tracking events are the same for both services. For information about migrating from {{site.data.keyword.at_full_notm}} to {{site.data.keyword.logs_full_notm}} and running the services in parallel, see [migration planning](/docs/cloud-logs?topic=cloud-logs-migration-intro).
{: important}

## Locations where activity tracking events are generated
{: #at-locations}


### Locations where activity tracking events are sent to {{site.data.keyword.at_full_notm}} hosted event search
{: #at-legacy-locations}


{{site.data.keyword.appconfig_short}} sends activity tracking events to {{site.data.keyword.at_full_notm}} hosted event search in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [Yes]{: tag-green}  | [Yes]{: tag-green}| [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #at-table-1}
{: tab-title="Americas"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #at-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green}| [No]{: tag-green} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #at-table-3}
{: tab-title="Europe"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

### Locations where activity tracking events are sent by {{site.data.keyword.atracker_full_notm}}
{: #atracker-locations}


{{site.data.keyword.appconfig_short}} sends activity tracking events by {{site.data.keyword.atracker_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #atracker-table-1}
{: tab-title="Americas"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #atracker-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green}| [No]{: tag-green} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #atracker-table-3}
{: tab-title="Europe"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}


## Viewing activity tracking events for {{site.data.keyword.appconfig_short}}
{: #at-viewing}

Events that are generated by {{site.data.keyword.appconfig_short}} are automatically forwarded to the {{site.data.keyword.at_full_notm}} service instance available in the same location.

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_full_notm}} service in the same location where your service instance is available.

1. Create a service instance of [{{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started).

1. [Start the {{site.data.keyword.at_full_notm}} web console](/docs/activity-tracker?topic=activity-tracker-launch) to access your events.


### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}



For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch).



## List of data events
{: #at_actions_data}

The following list of {{site.data.keyword.appconfig_short}} events is sent to {{site.data.keyword.at_full_notm}}.

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
| `apprapp.config-aggregator-settings.update` | Updates the configuration aggregator recording set-up and allows to either enable or disable the feature or failed to update |
| `apprapp.config-aggregator-settings.list` | Called to view the settings configuration or failed to list |
| `apprapp.config-aggregator-status.list` | Called to view status and time when the last configuration got updated or failed to list. |
| `apprapp.config-aggregator.query` | Called to list the resource configurations. |
{: caption="Actions that generate data events" caption-side="bottom"}

If an unauthorized request is made for any of the actions in table 3, a management event with reason code 403 is emitted.
{: note}
