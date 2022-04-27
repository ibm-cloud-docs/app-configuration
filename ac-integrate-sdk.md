---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-26"

keywords: app-configuration, app configuration, integrate sdk, node sdk, npm, sdk, android sdk, android, python sdk, python, go, golang, java server sdk, java, go admin sdk

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Integrating SDKs
{: #ac-sdks}

 The {{site.data.keyword.appconfig_short}} client SDK is available for Android, the server SDKs for Node, Python, Go, and Java, and the admin SDK for Go, to integrate with your web and mobile applications, microservices, and distributed environments.
{: shortdesc}

## Client-side and Server-side SDKs
{: #ac-sdk-types}

Understand the differences between the various SDKs so that you can decide between SDK types for your use case.

### Types of SDKs
{: #ac-sdk-types-of}

SDKs supported by {{site.data.keyword.appconfig_short}} include:

- Server-side SDK
- Client-side SDK
- Admin SDK

SDKs that help evaluate feature flag and property values are broadly classified as Server-side or Client-side - based on the deployment environment. These SDKs can be integrated into your application to assess the feature or property values by considering segment targeting rules, if any.

Evaluation SDKs fetch the latest configuration data from the {{site.data.keyword.appconfig_short}} service and ensure that any change in the service configuration is made available to your application in real time.

Admin SDKs can be used to create and manage configurations for Environments, Collections, Feature flags, Properties, and Segments. As an option to {{site.data.keyword.Bluemix_notm}} Dashboard or {{site.data.keyword.Bluemix_notm}} CLI, Admin SDKs can be used to programmatically manage your service configuration from within your application.

The currently available Go language Admin SDK integrates with your Go application.

**Differences between client-side and server-side SDKs:**

|SDK type |Details |Links to SDKs and integration docs |
| -- | -- | -- |
|Server side|These SDKs are designed for multi-user systems and are intended to be used in a trusted environment, such as inside a corporate network or on a web server.|[Node SDK](https://github.com/IBM/appconfiguration-node-sdk){: external}</br>[Documentation](/docs/app-configuration?topic=app-configuration-ac-integrate-sdks)</br>[Python SDK](https://github.com/IBM/appconfiguration-python-sdk){: external}</br>[Documentation](/docs/app-configuration?topic=app-configuration-ac-python)</br>[Go SDK](https://github.com/IBM/appconfiguration-go-sdk){: external}</br>[Documentation](/docs/app-configuration?topic=app-configuration-ac-golang)</br>[Java SDK](https://github.com/IBM/appconfiguration-java-sdk){: external}</br>[Documentation](/docs/app-configuration?topic=app-configuration-ac-java) |
|Client side|These SDKs are designed for single-user desktop, mobile, and embedded applications. Currently, {{site.data.keyword.appconfig_short}} Android SDK can be integrated with mobile applications.|[Android SDK](https://github.com/IBM/appconfiguration-android-client-sdk){: external}</br>[Documentation](/docs/app-configuration?topic=app-configuration-ac-integrate-sdks-android)|
|Admin SDK|Admin SDK is designed to perform {{site.data.keyword.appconfig_short}} service instance management. Use this SDK to create and manage {{site.data.keyword.appconfig_short}} resources like Collections, Environments, Feature flags, and Properties.|[App Configuration Admin SDK for Go](https://cloud.ibm.com/apidocs/app-configuration?code=go)|
{: caption="Table 1. List of {{site.data.keyword.appconfig_short}} server, client, and admin SDKs" caption-side="bottom"}

For more information about installation and technical concepts, see the 'readme file' document in the SDK.

You can also access these documents and download the SDKs from the {{site.data.keyword.appconfig_short}} console under SDKs on the navigation menu.
{: note}
