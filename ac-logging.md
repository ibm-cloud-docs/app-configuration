---

copyright:

  years: 2018, 2025
lastupdated: "2025-07-30"

keywords: app configuration cloud logs, app configuration logging, app configuration external logs

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Logging for {{site.data.keyword.appconfig_short}}
{: #logging}

{{site.data.keyword.cloud}} services, such as {{site.data.keyword.appconfig_short}}, generate platform logs that you can use to investigate abnormal activity and critical actions in your account, and troubleshoot problems.
{: shortdesc}

You can use {{site.data.keyword.logs_routing_full_notm}}, a platform service, to route platform logs in your account to a destination of your choice by configuring a tenant that defines where platform logs are sent. For more information, see [About Logs Routing](/docs/logs-router?topic=logs-router-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on platform logs that are generated in your account and routed by {{site.data.keyword.logs_routing_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

## Locations where platform logs are generated
{: #log-locations}

| Region                  | Supported                 |
|------------------------|----------------------|
| Dallas (`us-south`) | [Yes]{: tag-green} |
| Washington (`us-east`) | [Yes]{: tag-green} |
| Sydney (`au-syd`) | [Yes]{: tag-green} |
| Frankfurt (`eu-de`) | [Yes]{: tag-green} |
| London (`eu-gb`) | [Yes]{: tag-green} |
| Madrid (`eu-es`) | [Yes]{: tag-green} |
| Toronto (`ca-tor`) | [Yes]{: tag-green} |
| Tokyo (`jp-tok`) | [Yes]{: tag-green} |
| Osaka (`jp-osa`) | [Yes]{: tag-green} |
| Sao Paulo (`br-sao`) | [Yes]{: tag-green} |
| Montreal (`ca-mon`) | [Yes]{: tag-green} |
{: caption="Locations where platform logs are generated" caption-side="top"}


### Locations where logs are sent to {{site.data.keyword.logs_full_notm}}
{: #logs-locations}

{{site.data.keyword.appconfig_short}} sends platform logs to {{site.data.keyword.logs_full_notm}} in the regions indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) | Montreal (`ca-mon`) |
|---------------------|-------------------------|-------------------|----------------------|----------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where platform logs are sent in Americas locations" caption-side="top"}
{: #logs-table-1}
{: tab-title="Americas"}
{: tab-group="logs"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} |
{: caption="Regions where platform logs are sent in Asia Pacific locations" caption-side="top"}
{: #logs-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="logs"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where platform logs are sent in Europe locations" caption-side="top"}
{: #logs-table-3}
{: tab-title="Europe"}
{: tab-group="logs"}
{: class="simple-tab-table"}
{: row-headers}


## Locations where logs are sent by {{site.data.keyword.logs_routing_full_notm}}
{: #lr-locations}

{{site.data.keyword.appconfig_short}} sends logs by {{site.data.keyword.logs_routing_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) | Montreal (`ca-mon`) |
|---------------------|-------------------------|-------------------|----------------------|----------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where platform logs are sent in Americas locations" caption-side="top"}
{: #lr-table-1}
{: tab-title="Americas"}
{: tab-group="lr"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} |
{: caption="Regions where platform logs are sent in Asia Pacific locations" caption-side="top"}
{: #lr-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="lr"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where platform logs are sent in Europe locations" caption-side="top"}
{: #lr-table-3}
{: tab-title="Europe"}
{: tab-group="lr"}
{: class="simple-tab-table"}
{: row-headers}


## Enabling logging
{: #log-enable}

Platform logs are logs that are exposed by logging-enabled services and the platform in {{site.data.keyword.cloud_notm}}. You can configure {{site.data.keyword.cloud_notm}} logs instance to receive the logs sent by service. See [{{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-getting-started) for more information.

## Viewing logs
{: #logging_view-old}

To view and analyze platform logs for an {{site.data.keyword.appconfig_short}} instance, check that the {{site.data.keyword.logs_routing_full_notm}} instance is provisioned and target is set for the same region where the {{site.data.keyword.appconfig_short}} instance that you want to monitor is available.
{: note}

To start the {{site.data.keyword.logs_routing_full_notm}} web UI to view logs, see [Navigating to the web UI](/docs/cloud-logs?topic=cloud-logs-instance-launch).

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}

For more information about launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

## Fields per log type
{: #logging_fields-old}

See the following table for the list of fields that are included in each log record:

| Field             | Type       | Description             |
|-------------------|------------|-------------------------|
| `logSourceCRN`    | Required   | Defines the account where the log is published. |
| `saveServiceCopy` | Required   | Defines whether IBM saves a copy of the record for operational purposes. |
| `message`         | Required   | Description of the log that is generated.
| `msg_timestamp`   | Required   | UTC timestamp of the message.
| `messageID`       | Required   | ID of the log that is generated. |
| `documentsURL`    | Optional   | More information on how to proceed if you receive this log record. |
| `level`           | Required   | Type of log. Valid values are `INFO`, `WARN`, `ERROR` |
| `requestID`       | Optional | ID of the request/event triggered by the customer |
| `correlationID`   | Optional | ID of another request/event that was triggered as a result of the event triggered by the customer |
| `resource_collection_enabled` | | The field denoting if the resource collection is enabled for the app configuration instance. |
| `app-configuration_instance_id` | | guid of the app configuration instance. |
{: caption="Log record fields" caption-side="top"}

For information about fields included in every platform log, see [Fields for platform logs](/docs/logs-router?topic=logs-router-about-platform-logs#about-platform-logs-2).

## Log messages
{: #log_messages}

The following table lists the message IDs that are generated by {{site.data.keyword.appconfig_short}}:

| Message ID | Log type    | Description |
|------------|-------------|-------------|
| `apprapp.00001E` | `ERROR` | Invalid trusted profile id. |
| `apprapp.00002E` | `ERROR` | Invalid Instance ID {instance_id}. Provided Instance ID is not found. |
| `apprapp.00003E` | `ERROR` |Unauthorised. Looks like you do not have access to requested resource or action is not permitted for the corresponding IAM role. If this is a shared resource, please check if access policies are rightly created. |
| `apprapp.00004E` | `ERROR` | Invalid Instance ID. Provided Instance ID is not found. |
| `apprapp.00005E` | `ERROR` | Invalid Resource Collection Enabled. |
| `apprapp.00006E` | `ERROR` | crn not found for instance id. |
| `apprapp.00007E` | `ERROR` | Account id not found for the given instance. |
| `apprapp.00008E` | `ERROR` | "Unable to fetch resource for the service : " + {service_name} + " and config type : " + {config_type}. |
| `apprapp.00009E` | `ERROR` | Invalid entries for the resource region. |
| `apprapp.00001I` | `INFO` | Reconcilliation Successful for the instance : {instance_id}. |
| `apprapp.00002I` | `INFO` | Successfully fetched the configurations of Query Response. Number of entries are : {total_number_of_entries}. |
| `apprapp.00003I` | `INFO` | Settings Updated. Reconcilliation Not Triggered. |
{: caption="Additional information about message IDs" caption-side="top"}

### List logs generated by a service
{: #logging_analyze_1-old}

If you want to view all the logs that are being generated for a particular instance, select the `guid` prefixed with "apprapp-" of that {{site.data.keyword.appconfig_short}} instance from left panel under subsystems and search the source in search bar.
