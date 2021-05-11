---

copyright:
  years: 2021
lastupdated: "2021-03-19"

keywords: app-configuration, app configuration, data model, high availability, ha

subcollection: app-configuration

---

{:codeblock: .codeblock}
{:external: target="_blank" .external}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Monitor {{site.data.keyword.appconfig_short}} service metrics with {{site.data.keyword.mon_full_notm}}
{: #ac-monitoring}

<!-- All IBM Cloud® general availability (GA) services have a Service Level Agreement of 99.99% availability.  -->

Use {{site.data.keyword.mon_full_notm}} to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams, and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards.

## Set up your {{site.data.keyword.mon_full_notm}} service instance
{: #setup-monitor}

To get started, you need to [provision IBM Cloud Monitoring ](https://cloud.ibm.com/catalog/services/ibm-cloud-monitoring?callback=/observe/monitoring/create) instance on your {{site.data.keyword.IBM}} account. For more information on provisioning a {{site.data.keyword.mon_full_notm}} instance, see [here. ](https://test.cloud.ibm.com/docs/monitoring?topic=monitoring-provision)


{Currently, {{site.data.keyword.mon_full_notm}} integration is available for {{site.data.keyword.appconfig_short}} service deployments according to the following table:

| Deployment region    | Monitoring region |
|-------------|-------------|
| Dallas| Dallas |
| London| London|
| Sydney| Sydney|

### Opting in to and enabling {{site.data.keyword.appconfig_short}} monitoring metrics

Before you can start using {{site.data.keyword.appconfig_short}} monitoring metrics, you must first opt in and then [enable platform metrics](https://test.cloud.ibm.com/docs/monitoring?topic=monitoring-platform_metrics_enabling)
{:note: .note}

You can configure only one instance of the {{site.data.keyword.mon_full_notm}} service per region to collect platform metrics.
 - To configure the {{site.data.keyword.mon_full_notm}} instance, you must turn on the platform metrics configuration setting.
 - If a monitoring instance in a region is already enabled to collect platform metrics, metrics from enabled-monitoring services are collected automatically and available for monitoring through this instance. For more information about enabled-monitoring services, see {{site.data.keyword.Bluemix}} services.

 To monitor platform metrics, check that the {{site.data.keyword.mon_full_notm}} instance is provisioned in the same region where the {{site.data.keyword.Bluemix_notm}} instance is provisioned.
 {:note: .note}

 ## Accessing your {{site.data.keyword.mon_full_notm}} metrics
 {: #access-monitor}

 1. Launch the [{{site.data.keyword.mon_full_notm}} web UI](https://test.cloud.ibm.com/docs/monitoring?topic=monitoring-launch)from the **Observability** page
 1. Click DASHBOARDS
 1. In the Default Dashboards section, expand IBM
 1. Choose the {{site.data.keyword.appconfig_short}} dashboard from the list
 Access your deployment's monitoring dashboard from {{site.data.keyword.mon_full_notm}} , it's in the sidebar, under IBM.
 Next, change the scope or make a copy of the default dashboard to monitor an {{site.data.keyword.appconfig_short}} service  instance.

 ## Metrics available
 {: metrics-by-plan}

Evaluation count per instance

| Metadata   | Description |
|-------------|-------------|
| `Metric Name` | `ibm_apprapp_instance_evaluation` |
| `Metric Type` | `counter`|
| `Value Type` | `none`|
| `Segment By` | `ibm_ctype`, `ibm_service_name`, `ibm_location`, `ibm_scope`, `ibm_service_instance`, `ibm_apprapp_instance_id` |
