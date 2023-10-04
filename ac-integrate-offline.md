---

copyright:
  years: 2020, 2023
lastupdated: "2023-10-04"

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

Refer to the [CLI reference document](https://{DomainName}/docs/app-configuration?topic=app-configuration-cli-plugin-app-configuration-cli){: external} for steps to install and configure {{site.data.keyword.appconfig_short}} CLI.

Retrieve the configuration in a file by using the command:

```sh
ibmcloud ac export [--file FILE]
```
{: pre}

## Command options
{: #ac-ibmcloud-ac-configure-command}

`--file FILE`
: Path to file where configuration is exported

## Enabling offline mode
{: #ac-offline-enable}

As part of {{site.data.keyword.appconfig_short}} SDK initialization, you can let the SDK read the configuration from the file.

For a Node.js SDK you can use the local configuration file as in the following example:

```javascript
const client = AppConfiguration.getInstance();
let region = AppConfiguration.REGION_US_SOUTH;
let guid = 'abc-def-xyz';
let apikey = 'j9qc-abc-z79';
let collectionId = '<collectionId>';
let environmentId = '<environmentId>';

client.init(region, guid, apikey)
client.setContext(collectionId, environmentId, {
    bootstrapFile: "path/to/configuration/file.json",
    liveConfigUpdateEnabled: false
})
```
{: codeblock}

For more information, see the respective SDK documentation.
{: note}
