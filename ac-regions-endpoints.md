---

copyright:
  years: 2021, 2025
lastupdated: "2025-07-30"

keywords: app-configuration, app configuration, regions, endpoints, private endpoints

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Regions and endpoints
{: #ac-regions-endpoints}

Review region and connectivity options for interacting with {{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_notm}}.
{: shortdesc}

## Available regions
{: #ac-regions}

{{site.data.keyword.appconfig_notm}} is available in the following regions:

- Dallas
- Washington DC
- London
- Sydney
- Frankfurt
- Madrid
- Toronto
- Tokyo
- Osaka
- Sao Paulo
- Montreal

You can create {{site.data.keyword.appconfig_notm}} resources in one of the supported {{site.data.keyword.cloud_notm}} regions.

## Service endpoints
{: #ac-endpoints}

{{site.data.keyword.appconfig_notm}} offers two connectivity options for interacting with its service APIs.

Public endpoints
:   By default, you can connect to resources in your account over the {{site.data.keyword.cloud_notm}} public network. Your data is encrypted in transit by using the Transport Security Layer (TLS) 1.2 protocol.

Private endpoints
:   To further secure your connection, you can also enable [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint) for your infrastructure account. When you enable VRF for your account, you can connect to {{site.data.keyword.appconfig_notm}} by using a private IP that is accessible only through the {{site.data.keyword.cloud_notm}} private network.

### Public endpoints
{: #ac-public-endpoints}

The following table contains the base URLs for the {{site.data.keyword.appconfig_notm}} API endpoints. When you call the API, use the URL that corresponds to the region where your service instance is deployed. Add the path for each method to form the complete API endpoint for your requests.

|Location     |Endpoint URL      |
|-------------|------------------|
|Dallas |`https://us-south.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Washington DC |`https://us-east.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|London |`https://eu-gb.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Sydney |`https://au-syd.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Frankfurt |`https://eu-de.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Madrid |`https://eu-es.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Toronto |`https://ca-tor.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Tokyo |`https://jp-tok.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Osaka |`https://jp-osa.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Sao Paulo |`https://br-sao.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Montreal | `https://ca-mon.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
{: caption="Public endpoints" caption-side="top"}

### Private endpoints
{: #ac-private-endpoints}

If you need to manage your {{site.data.keyword.appconfig_notm}} resources over a private network, see the following table to determine the API endpoints to use when you connect to the {{site.data.keyword.appconfig_notm}} API.

|Location     |Endpoint URL      |
|-------------|------------------|
|Dallas |`https://private.us-south.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Washington DC |`https://private.us-east.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|London |`https://private.eu-gb.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Sydney |`https://private.au-syd.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Frankfurt |`https://private.eu-de.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Madrid |`https://private.eu-es.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Toronto |`https://private.ca-tor.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Tokyo |`https://private.jp-tok.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Osaka |`https://private.jp-osa.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Sao Paulo |`https://private.br-sao.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
|Montreal | `https://ca-mon.apprapp.cloud.ibm.com/apprapp/feature/v1/instances/{guid}` |
{: caption="Private endpoints" caption-side="top"}
