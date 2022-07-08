---

copyright:
  years: 2020, 2022
lastupdated: "2022-07-08"

keywords: app-configuration, app configuration, integrate sdk, node sdk, npm, sdk, android sdk, android, python sdk, python, go, golang, java server sdk, java, go admin sdk

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Enable offline mode
{: #ac-offline}

## Benefits of offline mode
{: #ac-offline-benefits}

Enabling offline mode lets you evaluate feature flags or properties when the application is running in an air-gapped environment.  

This method allows the application to use {{site.data.keyword.appconfig_short}} SDK and evaluate the feature flags and properties in a highly secure system such as FedRAMP compliant systems. It also helps to achieve GitOps operational procedures, which rely on Git as a source control system.

## Creating the configuration file to use in offline mode
{: #ac-offline-configfile}

To enable offline mode, use a local file with the configuration details. You can create this file by using the {{site.data.keyword.appconfig_short}} CLI.

Refer to the [CLI reference document](https://cloud.ibm.com/docs/app-configuration?topic=app-configuration-cli-plugin-app-configuration-cli) for steps to install and configure {{site.data.keyword.appconfig_short}} CLI.

Retrieve the configuration in a file by using the command:

```sh
ibmcloud ac config --collection_id COLLECTION_ID --environment_id ENVIRONMENT_ID [--file FILE]
```
{: pre}

## Command options
{: #ac-ibmcloud-ac-configure-command}

`--environment_id ENVIRONMENT_ID`
: Environment ID

`--collection_id COLLECTION_ID`
: Collection ID

`--file FILE`
: Path to file where configuration is exported

## Enabling offline mode
{: #ac-offline-enable}

As part of {{site.data.keyword.appconfig_short}} SDK initialization, you can let the SDK read the configuration from the file.  

For a Node.js SDK you can use the local configuration file as in the following example:

```javascript
const client = AppConfiguration.getInstance();
let region = AppConfiguration.REGION_US_SOUTH;
let guid = 'abc-def-xyz'; let apikey = 'j9qc-abc-z79';
client.init(region, guid, apikey)
let collectionId = '<collectionId>';
let environmentId = '<environmentId>';
let configurationFile = 'path/to/configuration/file.json';
let liveConfigUpdateEnabled = false;
client.setContext(collectionId, environmentId, configurationFile, liveConfigUpdateEnabled)
```
{: codeblock}

For more information, see the respective SDK documentation.
{: note}
