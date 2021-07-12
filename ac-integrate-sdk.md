---

copyright:
  years: 2020, 2021
lastupdated: "2021-03-29"

keywords: app-configuration, app configuration, integrate sdk, node sdk, npm, sdk, android sdk, android, python sdk, python, go, golang, java server sdk, java, go admin sdk

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
{:java: .ph data-hd-programlang='java'}
{:ruby: .ph data-hd-programlang='ruby'}
{:c#: .ph data-hd-programlang='c#'}
{:objectc: .ph data-hd-programlang='Objective C'}
{:python: .ph data-hd-programlang='python'}
{:javascript: .ph data-hd-programlang='javascript'}
{:php: .ph data-hd-programlang='PHP'}
{:swift: .ph data-hd-programlang='swift'}
{:reactnative: .ph data-hd-programlang='React Native'}
{:csharp: .ph data-hd-programlang='csharp'}
{:ios: .ph data-hd-programlang='iOS'}
{:android: .ph data-hd-programlang='Android'}
{:cordova: .ph data-hd-programlang='Cordova'}
{:xml: .ph data-hd-programlang='xml'}
{:curl: .ph data-hd-programlang='curl'}
{:node: .ph data-hd-programlang='node'}

# Integrating SDKs
{: #ac-sdks}

Following are the list of {{site.data.keyword.appconfig_short}} client, server, and admin SDKs. The {{site.data.keyword.appconfig_short}} client SDK is available for Android, the server SDKs for Node, Python, Go, and Java, and the admin SDK for Go, to integrate with your web and mobile applications, microservices, and distributed environments.
{:shortdesc}

For more information about installation and technical concepts, see the 'readme file' document in the SDK.

|Server SDKs                          |Client SDKs                          |Admin SDKs                          |
|-------------------------------------|-------------------------------------|------------------------------------|
|[Node SDK](https://github.com/IBM/appconfiguration-node-sdk){: external} </br>[Node SDK documentation](/docs/app-configuration?topic=app-configuration-ac-integrate-sdks) |[Android SDK](https://github.com/IBM/appconfiguration-android-client-sdk){: external} </br>[Android SDK documentation](/docs/app-configuration?topic=app-configuration-ac-integrate-sdks-android) |[Go Admin SDK](https://github.com/IBM/appconfiguration-go-admin-sdk){: external} </br>[Go Admin SDK documentation](https://{DomainName}/apidocs/app-configuration?code=go) |
|[Python SDK](https://github.com/IBM/appconfiguration-python-sdk){: external} </br>[Python SDK documentation](/docs/app-configuration?topic=app-configuration-ac-python) | &nbsp;&nbsp; | &nbsp;&nbsp; |
|[Go SDK](https://github.com/IBM/appconfiguration-go-sdk){: external} </br>[Go SDK documentation](/docs/app-configuration?topic=app-configuration-ac-golang) | &nbsp;&nbsp; | &nbsp;&nbsp; |
|[Java SDK](https://github.com/IBM/appconfiguration-java-sdk){: external} </br>[Java SDK documentation](/docs/app-configuration?topic=app-configuration-ac-java) | &nbsp;&nbsp; | &nbsp;&nbsp; |
{:caption="Table 1. List of {{site.data.keyword.appconfig_short}} server, client, and admin SDKs" caption-side="top"}

You can also access these documents and download the SDKs from the {{site.data.keyword.appconfig_short}} console under SDKs on the navigation menu.
{: note}

## Offline mode
{: #ac-offline}

### Benefits of offline mode
{: #ac-offline-benefits}

Enabling offline mode lets you evaluate feature flags or properties when the application is running in an air-gapped environment.  

This method allows the application to use {{site.data.keyword.appconfig_short}} SDK and evaluate the feature flags and properties in a highly secure system such as FedRAMP compliant systems. It also helps to achieve GitOps operational procedures, which rely on Git as a source control system.

### Creating the configuration file to use in offline mode
{: #ac-offline-configfile}

To enable offline mode, use a local file with the configuration details. You can create this file that uses the {{site.data.keyword.appconfig_short}} CLI.

Refer to the [CLI reference document](https://cloud.ibm.com/docs/app-configuration?topic=app-configuration-cli-plugin-app-configuration-cli) for steps to install and configure {{site.data.keyword.appconfig_short}} CLI.

Retrieve the configuration in a file by using the command:

```sh
ibmcloud ac config --collection_id COLLECTION_ID --environment_id ENVIRONMENT_ID [--file FILE]
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-configure-command}

<dl>
<dt>--environment_id ENVIRONMENT_ID</dt>
<dd>Environment Id</dd>
<dt>--collection_id COLLECTION_ID</dt>
<dd>Collection Id</dd>
<dt>--file FILE</dt>
<dd>Path to file where configuration is exported./dd>
</dl>

### Enabling offline mode
{: #ac-offline-enable}

As part of {{site.data.keyword.appconfig_short}} SDK initialization, you can let the SDK read the configuration from the file.  

For a Node.js SDK you can use the local configuration file as in the following example:

```javascript
const client = AppConfiguration.getInstance();
let region = AppConfiguration.REGION_US_SOUTH;;
let guid = 'abc-def-xyz'; let apikey = 'j9qc-abc-z79';
client.init(region, guid, apikey)
let collectionId = '<collectionId>';
let environmentId = '<environmentId>';
let configurationFile = 'path/to/configuration/file.json';
let liveConfigUpdateEnabled = false;
client.setContext(collectionId, environmentId, configurationFile, liveConfigUpdateEnabled)
```
{: codeblock}

Refer to the respective SDK documentation for specific guidance.
{: note}
