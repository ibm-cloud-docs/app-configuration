---

copyright:
  years: 2024
lastupdated: "2024-11-11"

keywords:

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Understanding data portability for {{site.data.keyword.appconfig_notm}}
{: #data-portability}

Data portability involves a set of tools and procedures that enable customers to export the digital artifacts that are needed to implement similar workload and data processing on different service providers or on-premises software. It includes procedures for copying and storing the service customer content, including the related configuration that is used by the service to store and process the data, on the customer's own location.
{: shortdesc}

## Responsibilities
{: #data-portability-responsibilities}

{{site.data.keyword.cloud_notm}} services provide interfaces and instructions to guide the customer to copy and store the service customer content, including the related configuration, on their own selected location.
{: shortdesc}

The customer is responsible for the use of the exported data and configuration for data portability to other infrastructures, which includes:

- The planning and execution for setting up alternative infrastructure on different cloud providers or on-premises software that provide similar capabilities to the {{site.data.keyword.IBM_notm}} services.
- The planning and execution for the porting of the required application code on the alternative infrastructure, including the adaptation of customer's application code, deployment automation.
- The conversion of the exported data and configuration to the format that is required by the alternative infrastructure and adapted applications.

For more information about your responsibilities for {{site.data.keyword.appconfig}}, see [Shared responsibilities for {{site.data.keyword.appconfig_notm}}](/docs/app-configuration?topic=app-configuration-ac-responsibilities).

## Data export procedures
{: #data-portability-procedures}

All data available within the {{site.data.keyword.appconfig_notm}} service data can be accessed by using the [API documentation](/apidocs/app-configuration). The customer can export the complete customer metadata and the service configurations by using the [export instance configuration](/apidocs/app-configuration#list-instance-config).

## Exported data formats
{: #data-portability-data-formats}

{{site.data.keyword.appconfig_notm}} resources export the data via Service APIs in JSON format. The schema of the exported data is described in the {{site.data.keyword.appconfig_notm}} service [API documentation](https://cloud.ibm.com/apidocs/app-configuration).

## Data ownership
{: #data-portability-ownership}

All exported data is classified as customer content and is therefore applied to them full customer ownership and licensing rights, as stated in [{{site.data.keyword.cloud_notm}} Service Agreement](https://www.ibm.com/support/customer/csol/terms/?id=Z126-6304_WS&cc=in&lc=en){: external}.
