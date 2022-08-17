---

copyright:
  years: 2020, 2022
lastupdated: "2022-08-17"

keywords: app-configuration, app configuration, integrate sdk, node sdk, npm

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# App Configuration server SDK for Node
{: #ac-integrate-sdks}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Node.js microservice or application.
{: shortdesc}

Version v0.4.0 has changes to the return value of `getCurrentValue` method. Hence, if you are already using a version below v0.4.0, read the [migration guide](https://github.ibm.com/devx-app-services/appconfiguration-node-sdk/blob/development/docs/v0.3-v0.4.md) before you upgrade the SDK to latest.
{: important}

## Integrating server SDK for Node
{: #ac-integrate-ff-sdk}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Node.js microservice or application. You can evaluate the values of your feature flag and property by integrating the {{site.data.keyword.appconfig_short}} SDK.

1. Install the SDK. Use the following code from the `npm` registry.

   ```bash
   npm install ibm-appconfiguration-node-sdk@latest
   ```
   {: codeblock}

1. In your Node.js microservice, include the SDK module with:

   ```javascript
   const {
     AppConfiguration
   } = require('ibm-appconfiguration-node-sdk');
   ```
   {: codeblock}

1. Initialize the sdk to connect with your {{site.data.keyword.appconfig_short}} service instance.
   {: #ac-init-node-sdk}

   ```javascript
   const region = AppConfiguration.REGION_US_SOUTH;;
   const guid = '<guid>';
   const apikey = '<apikey>';

   const collectionId = '<collectionId>';
   const environmentId = '<environmentId>';

   const appConfigClient = AppConfiguration.getInstance();
   appConfigClient.init(region, guid, apikey)
   appConfigClient.setContext(collectionId, environmentId)
   ```
   {: codeblock}

   Where:
   - `region`: Region name where the service instance is created. Use `AppConfiguration.REGION_US_SOUTH` for Dallas, `AppConfiguration.REGION_EU_GB` for London, `AppConfiguration.REGION_AU_SYD` for Sydney, and `AppConfiguration.REGION_US_EAST` for Washington DC.
   - `guid`: Instance ID of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} dashboard.
   - `apikey`: ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} dashboard.
   - `collectionId`: ID of the collection created in App Configuration service instance under the Collections section.
   - `environmentId`: ID of the environment created in App Configuration service instance under the Environments section.

   The `init()` and `setContext()` are the initialization methods and should be invoked only once using `appConfigClient`. The `appConfigClient`, once initialized, can be obtained across modules using `AppConfiguration.getInstance()`.
   {: note}

### Option to use a persistent cache for configuration
{: #ac-init-cache-node-sdk}

In order for your application and SDK to continue its operations during the unlikely unavailability of the {{site.data.keyword.appconfig_short}} server, you can configure the SDK to use a persistent cache. The SDK uses the persistent cache to store {{site.data.keyword.appconfig_short}} data that is available across your application restarts.

```javascript
// 1. default (without persistent cache)
appConfigClient.setContext(collectionId, environmentId)

// 2. with persistent cache
appConfigClient.setContext(collectionId, environmentId, {
   persistentCacheDirectory: '/var/lib/docker/volumes/'
})
```
{: codeblock}

Where:
- `persistentCacheDirectory`: Absolute path to a directory, which has read and write permission for the user. The SDK creates a file - `AppConfiguration.json` in the specified directory, and it is used as the persistent cache to store the {{site.data.keyword.appconfig_short}} service information.

   When persistent cache is enabled, the SDK keeps the last known good configuration in the persistent cache. If the {{site.data.keyword.appconfig_short}} server is unreachable, the most recent configurations in the persistent cache are loaded to the application to continue working.

Make sure that the cache file is not lost or deleted in any case. For example, consider the case when a kubernetes pod is restarted and the cache file (appconfiguration.json) was stored in ephemeral volume of the pod. As pod gets restarted, kubernetes destroys the ephermal volume in the pod, as a result the cache file gets deleted. So, make sure that the cache file created by the SDK is always stored in persistent volume by providing the correct absolute path of the persistent directory.
{: important}

### Offline options
{: #ac-offline-node-sdk}

The SDK is also designed to serve configurations, perform feature flag and property evaluations without being connected to {{site.data.keyword.appconfig_short}} service.

```javascript
appConfigClient.setContext(collectionId, environmentId, {
   bootstrapFile: 'saflights/flights.json',
   liveConfigUpdateEnabled: false
})
```
{: codeblock}

Where:
- `bootstrapFile`: Absolute path of the JSON file, which contains configuration details. Make sure to provide a proper JSON file. You can generate this file by using `ibmcloud ac config` command of the {{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_short}} CLI.
- `liveConfigUpdateEnabled`: Live configuration update from the server. Set this value to `false` if the new configuration values are not to be fetched from the server.

### Examples for using feature and property-related APIs
{: #ac-integrate-ff-example}

See the following examples for using the feature-related APIs.

#### Get single feature
{: #ac-integrate-ff-get-single-feature}

```javascript
const feature = appConfigClient.getFeature('online-check-in'); // feature can be null incase of an invalid feature id

if (feature != null) {
  console.log(`Feature Name ${feature.getFeatureName()} `);
  console.log(`Feature Id ${feature.getFeatureId()} `);
  console.log(`Feature Type ${feature.getFeatureDataType()} `);
  if (feature.isEnabled()) {
    // feature flag is enabled
  } else {
    // feature flag is disabled
  }
}
```
{: codeblock}

#### Get all features
{: #ac-integrate-ff-get-all-features}

```javascript
const features = appConfigClient.getFeatures();
const feature = features['online-check-in'];

if (feature != null) {
  console.log(`Feature Name ${feature.getFeatureName()} `);
  console.log(`Feature Id ${feature.getFeatureId()} `);
  console.log(`Feature Type ${feature.getFeatureDataType()} `);
  console.log(`Is feature enabled? ${feature.isEnabled()} `);
}
```
{: codeblock}

#### Feature evaluation
{: #ac-integrate-ff-feature-evaluation}

You can use the `feature.getCurrentValue(entityId, entityAttributes)` method to evaluate the value of the feature flag. This method returns an JSON object containing evaluated value, feature flag enabled status and evaluation details.

```javascript
const entityId = '<entityId>';
const entityAttributes = {
  city: 'Bangalore',
  country: 'India',
};

const result = feature.getCurrentValue(entityId, entityAttributes);
console.log(result.value); // Evaluated value of the feature flag. The type of evaluated value will match the type of feature flag (Boolean, String, Numeric).
console.log(result.isEnabled); // enabled status.
console.log(result.details); // a JSON object containing detailed information of the evaluation. See below

// the `result.details` will have the following
console.log(result.details.valueType); // a string value. Example: DISABLED_VALUE
console.log(result.details.reason); // a string value. Example: Disabled value of the feature flag since the feature flag is disabled.
console.log(result.details.segmentName); // (only if applicable, else it is undefined) a string value containing the segment name for which the feature flag was evaluated.
console.log(result.details.rolloutPercentageApplied); // (only if applicable, else it is undefined) a boolean value. True if the entityId was part of the rollout percentage evaluation, false otherwise.
console.log(result.details.errorType); // (only if applicable, else it is undefined) contains the error.message if any error was occured during the evaluation.
```
{: codeblock}

- `entityId`: Id of the entity. This will be a string identifier related to the entity against which the feature is evaluated. For example, an entity might be an instance of an app that runs on a mobile device, a microservice that runs on the cloud, or a component of infrastructure that runs that microservice. For any entity to interact with {{site.data.keyword.appconfig_short}}, it must provide a unique entity ID.

- `entityAttributes`: A JSON object consisting of the attribute name and their values that defines the specified entity. This is an optional parameter if the feature flag is not configured with any targeting definition. If the targeting is configured, then `entityAttributes` should be provided for the rule evaluation. An attribute is a parameter that is used to define a segment. The SDK uses the attribute values to determine if the specified entity satisfies the targeting rules, and returns the appropriate feature flag value.

#### Get single property
{: #ac-integrate-ff-get-single-property}

```javascript
const property = appConfigClient.getProperty('property_id'); // property can be null incase of an invalid property id

if (property != null) {
  console.log(`Property Name ${property.getPropertyName()} `);
  console.log(`Property Id ${property.getPropertyId()} `);
  console.log(`Property Type ${property.getPropertyDataType()} `);
}
```
{: codeblock}

#### Get all properties
{: #ac-integrate-ff-get-all-properties}

```javascript
const properties = appConfigClient.getProperties();
const property = properties['property_id'];

if (property != null) {
  console.log(`Property Name ${property.getPropertyName()} `);
  console.log(`Property Id ${property.getPropertyId()} `);
  console.log(`Property Type ${property.getPropertyDataType()} `);
}
```
{: codeblock}

#### Evaluate a property
{: #ac-integrate-ff-property-evaluation}

You can use the `property.getCurrentValue(entityId, entityAttributes)` method to evaluate the value of the property. This method returns an JSON object containing evaluated value and evaluation details.

```javascript
const entityId = '<entityId>';
const entityAttributes = {
  city: 'Bangalore',
  country: 'India',
};

const result = property.getCurrentValue(entityId, entityAttributes);
console.log(result.value); // Evaluated value of the property. The type of evaluated value will match the type of property (Boolean, String, Numeric).
console.log(result.details); // a JSON object containing detailed information of the evaluation. See below

// the `result.details` will have the following
console.log(result.details.valueType); // a string value. Example: DEFAULT_VALUE
console.log(result.details.reason); // a string value. Example: Default value of the property.
console.log(result.details.segmentName); // (only if applicable, else it is undefined) a string value containing the segment name for which the property was evaluated.
console.log(result.details.errorType); // (only if applicable, else it is undefined) contains the error.message if any error was occured during the evaluation.
```
{: codeblock}

- `entityId`: Id of the entity. This will be a string identifier related to the entity against which the property is evaluated. For example, an entity might be an instance of an app that runs on a mobile device, a microservice that runs on the cloud, or a component of infrastructure that runs that microservice. For any entity to interact with {{site.data.keyword.appconfig_short}}, it must provide a unique entity ID.

- `entityAttributes`: A JSON object consisting of the attribute name and their values that defines the specified entity. This is an optional parameter if the property is not configured with any targeting definition. If the targeting is configured, then `entityAttributes` should be provided for the rule evaluation. An attribute is a parameter that is used to define a segment. The SDK uses the attribute values to determine if the specified entity satisfies the targeting rules, and returns the appropriate property value.

## Fetching the appConfigClient across other modules
{: #ac-fetch-appconfigclient-across-modules}

Once the SDK is initialized, the `appConfigClient` can be obtained across other modules as shown below:

```javascript
// **other modules**

const { AppConfiguration } = require('ibm-appconfiguration-node-sdk');
const appConfigClient = AppConfiguration.getInstance();

feature = appConfigClient.getFeature('online-check-in');
const enabled = feature.isEnabled();
const featureValue = feature.getCurrentValue(entityId, entityAttributes)
```
{: codeblock}

## Supported data types
{: #ac-integrate-ff-supported-data-types}

You can configure feature flags and properties with {{site.data.keyword.appconfig_short}}, supporting the following data types: Boolean, Numeric, and String. The String data type can be in the format of a text string, JSON, or YAML. The SDK processes each format as shown in the table.

| **Feature or Property value** | **Data type** | **Data format** | **Type of data returned by `getCurrentValue()`** | **Example output** |
| -- | -- | -- | -- | -- |
| `true` | BOOLEAN | not applicable | `boolean` | `true` |
| `25` | NUMERIC | not applicable | `number` | `25` |
| "a string text" | STRING | TEXT | `string` | `a string text` |
| `{"firefox": {`  \n `"name": "Firefox",`  \n  `"pref_url": "about:config"`  \n }} | STRING | JSON | `org.json.JSONObject` | `{"firefox":{"name":"Firefox","pref_url":"about:config"}}` |
|  `men:`  \n   `- John Smith`   \n`- Bill Jones`\n `women:`  \n   `- Mary Smith`   \n`- Susan Williams` | STRING | YAML | `java.lang.String` | `"men:\n  - John Smith\n  - Bill Jones\women:\n  - Mary Smith\n  - Susan Williams"`  |
{: caption="Table 1. Example outputs" caption-side="bottom"}

### Feature flag
{: #ac-integrate-ff-feature-flag}

```javascript
const feature = appConfigClient.getFeature('json-feature');
feature.getFeatureDataType(); // STRING
feature.getFeatureDataFormat(); // JSON

// Example (traversing the returned JSON)
let result = feature.getCurrentValue(entityId, entityAttributes);
console.log(result.value.key) // prints the value of the key

const feature = appConfigClient.getFeature('yaml-feature');
feature.getFeatureDataType(); // STRING
feature.getFeatureDataFormat(); // YAML
feature.getCurrentValue(entityId, entityAttributes);
```
{: codeblock}

### Property
{: #ac-integrate-ff-property}

```javascript
const property = appConfigClient.getProperty('json-property');
property.getPropertyDataType(); // STRING
property.getPropertyDataFormat(); // JSON

// Example (traversing the returned JSON)
let result = property.getCurrentValue(entityId, entityAttributes);
console.log(result.value.key) // prints the value of the key

const property = appConfigClient.getProperty('yaml-property');
property.getPropertyDataType(); // STRING
property.getPropertyDataFormat(); // YAML
property.getCurrentValue(entityId, entityAttributes);
```
{: codeblock}

### Listen to the feature or property changes
{: #ac-integrate-ff-feature-prop-change}

The SDK provides an event-based mechanism to notify you in real-time when feature flag's or property's configuration changes. You can listen to `configurationUpdate` event using the same `appConfigClient`.

```javascript
appConfigClient.emitter.on('configurationUpdate', () => {
  // **add your code**
  // To find the effect of any configuration changes, you can call the feature or property related methods

  // feature = appConfigClient.getFeature('online-check-in');
  // newValue = feature.getCurrentValue(entityId, entityAttributes);
});
```
{: codeblock}
