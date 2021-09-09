---

copyright:
  years: 2020, 2021
lastupdated: "2021-09-09"

keywords: app-configuration, app configuration, integrate sdk, node sdk, npm

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

# App Configuration server SDK for Node
{: #ac-integrate-sdks}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Node.js microservice or application.
{: shortdesc}

## Integrating server SDK for Node
{: #ac-integrate-ff-sdk}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Node.js microservice or application. You can evaluate the values of your feature flag and property by integrating the {{site.data.keyword.appconfig_short}} SDK.

1. Install the SDK using the following code from the `npm` registry.

   ```bash
   $ npm install ibm-appconfiguration-node-sdk
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
   const client = AppConfiguration.getInstance();

   let region = AppConfiguration.REGION_US_SOUTH;;
   let guid = 'abc-def-xyz';
   let apikey = 'j9qc-abc-z79';

   client.init(region, guid, apikey)

   let collectionId = '<collectionId>';
   let environmentId = '<environmentId>';
   client.setContext(collectionId, environmentId)
   ```
   {: codeblock}

   where,
   - region: Region name where the service instance is created. Use `AppConfiguration.REGION_US_SOUTH` for Dallas, `AppConfiguration.REGION_EU_GB` for London, and `AppConfiguration.REGION_AU_SYD` for Sydney.
   - guid: Instance Id of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - apikey: ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - collectionId: Id of the collection created in App Configuration service instance under the Collections section.
   - environmentId: Id of the environment created in App Configuration service instance under the Environments section.

   ### Option to use a persistent cache for configuration
   {: #ac-init-cache-node-sdk}

   In order for your application and SDK to continue its operations even during the unlikely scenario of App Configuration service going down, you can configure the SDK to work using a persistent cache. The SDK uses the persistent cache to store the App Configuration data that will be available across your application restarts.
   ```javascript
   // 1. default (without persistent cache)
   client.setContext(collectionId, environmentId)

   // 2. with persistent cache
   client.setContext(collectionId, environmentId, {
     persistentCacheDirectory: '/var/lib/docker/volumes/'
   })
   ```
   * persistentCacheDirectory: Absolute path to a directory which has read and write permission for the user. The SDK will create a file - `AppConfiguration.json` in the specified directory, and it will be used as the persistent cache to store the App Configuration service information.

   When persistent cache is enabled, the SDK will keep the last known good configuration at the persistent cache. In the case of App Configuration server being unreachable, the latest configurations in the persistent cache is loaded to the application to continue working.

   ### Offline options
   {: #ac-offline-node-sdk}

   The SDK is also designed to serve configurations, perform feature flag & property evaluations without being connected to App Configuration service.
   ```javascript
   client.setContext(collectionId, environmentId, {
     bootstrapFile: 'saflights/flights.json',
     liveConfigUpdateEnabled: false
   })
   ```
   * bootstrapFile: Absolute path of the JSON file, which contains configuration details. Make sure to provide a proper JSON file. You can generate this file using `ibmcloud ac config` command of the IBM Cloud App Configuration CLI.
   * liveConfigUpdateEnabled: Live configuration update from the server. Set this value to `false` if the new configuration values shouldn't be fetched from the server.


### Examples for using feature and property related APIs
{: #ac-integrate-ff-example}

Refer to the below examples for using the feature related APIs.

#### Get single feature
{: #ac-integrate-ff-get-single-feature}

```javascript
const feature = client.getFeature('feature_id')

if(feature) {

    if(feature.isEnabled()) {
        // enable feature
    } else {
        // disable the feature
    }
    console.log('data', feature);
    console.log(`Feature Name ${feature.getFeatureName()} `);
    console.log(`Feature Id ${feature.getFeatureId()} `);
    console.log(`Feature Type ${feature.getFeatureDataType()} `);
    console.log(`Feature is enabled ${feature.isEnabled()} `);
}
```
{: codeblock}

#### Get all features
{: #ac-integrate-ff-get-all-features}

```javascript
const features = client.getFeatures();

const feature = features["feature_id"];

if(feature) {
    console.log(`Feature Name ${feature.getFeatureName()}`);
    console.log(`Feature Id ${feature.getFeatureId()}`);
    console.log(`Feature Type ${feature.getFeatureDataType()}`);
    console.log(`Feature is enabled ${feature.isEnabled()}`);
}
```
{: codeblock}

#### Feature evaluation
{: #ac-integrate-ff-feature-evaluation}

You can use the `feature.getCurrentValue(entityId, entityAttributes)` method to evaluate the value of the feature flag. You should pass an unique `entityId` as the parameter to perform the feature flag evaluation.

##### Feature usage

* If the feature flag is configured with segments in the {{site.data.keyword.appconfig_short}} service, provide a JSON object as `entityAttributes` parameter to this method.

   ```javascript
    const entityId = 'john_doe';
    const entityAttributes = {
      city: 'Bangalore',
      country: 'India',
    };

    const featureValue = feature.getCurrentValue(entityId, entityAttributes);
   ```
   {: codeblock}

* If the feature flag is not targeted to any segments and the feature flag is turned **ON** this method returns the feature **enabled value**. And when the feature flag is turned **OFF** this method returns the feature **disabled value**.

   ```javascript
   const entityId = 'john_doe';
   const featureValue = feature.getCurrentValue(entityId);
   ```
   {: codeblock}

#### Get single property
{: #ac-integrate-ff-get-single-property}

```javascript
const property = client.getProperty('property_id')

if(property) {
    console.log('data', property);
    console.log(`Property Name ${property.getPropertyName()}`);
    console.log(`Property Id ${property.getPropertyId()}`);
    console.log(`Property Type ${property.getPropertyDataType()}`);
}
```
{: codeblock}

#### Get all properties
{: #ac-integrate-ff-get-all-properties}

```javascript
const properties = client.getProperties();

const property = properties["property_id"];

if(property) {
    console.log(`Property Name ${property.getPropertyName()}`);
    console.log(`Property Id ${property.getPropertyId()}`);
    console.log(`Property Type ${property.getPropertyDataType()}`);
}
```
{: codeblock}

#### Evaluate a property
{: #ac-integrate-ff-property-evaluation}

You can use the `property.getCurrentValue(entityId, entityAttributes)` method to evaluate the value of the property. You should pass an unique `entityId` as the parameter to perform the property evaluation.

##### Property usage

- If the property is configured with segments in the App Configuration service, provide a json object as `entityAttributes` parameter to this method.

   ```javascript
    const entityId = 'john_doe';
    const entityAttributes = {
      city: 'Bangalore',
      country: 'India',
    };

    const propertyValue = property.getCurrentValue(entityId, entityAttributes);    
   ```
   {: codeblock}

- If the property is not targeted to any segments, this method returns the property value.

   ```javascript
   const entityId = 'john_doe';
   const propertyValue = property.getCurrentValue(entityId);
   ```
   {: codeblock}


## Supported data types
{: #ac-integrate-ff-supported-data-types}

{{site.data.keyword.appconfig_short}} service allows you to configure feature flags and properties in the following data types: Boolean, Numeric, String. The String data type can be in the format of a text string, JSON, or YAML. The SDK processes each format accordingly as shown in the below table.

| **Feature or Property value**                                                                          | **DataType** | **DataFormat** | **Type of data returned <br> by `getCurrentValue()`** | **Example output**                                                   |
| ------------------------------------------------------------------------------------------------------ | ------------ | -------------- | ----------------------------------------------------- | -------------------------------------------------------------------- |
| `true`                                                                                                 | BOOLEAN      | not applicable | `boolean`                                                | `true`                                                               |
| `25`                                                                                                   | NUMERIC      | not applicable | `number`                                             | `25`                                                                 |
| "a string text"                                                                                        | STRING       | TEXT           | `string`                                              | `a string text`                                                      |
| <pre>{<br>  "firefox": {<br>    "name": "Firefox",<br>    "pref_url": "about:config"<br>  }<br>}</pre> | STRING       | JSON           | `JSON object`                              | `{"firefox":{"name":"Firefox","pref_url":"about:config"}}` |
| <pre>men:<br>  - John Smith<br>  - Bill Jones<br>women:<br>  - Mary Smith<br>  - Susan Williams</pre>  | STRING       | YAML           | `string`                              | `"men:\n  - John Smith\n  - Bill Jones\nwomen:\n  - Mary Smith\n  - Susan Williams"` |
{: caption="Table 1. Example outputs" caption-side="top"}


#### Feature flag

```javascript
  const feature = client.getFeature('json-feature');
  feature.getFeatureDataType(); // STRING
  feature.getFeatureDataFormat(); // JSON

  // Example (traversing the returned JSON)
  let result = feature.getCurrentValue(entityId, entityAttributes);
  console.log(result.key) // prints the value of the key

  const feature = client.getFeature('yaml-feature');
  feature.getFeatureDataType(); // STRING
  feature.getFeatureDataFormat(); // YAML
  feature.getCurrentValue(entityId, entityAttributes); // returns the stringified yaml (check above table)
```
{: codeblock}

#### Property

```javascript
  const property = client.getProperty('json-property');
  property.getPropertyDataType(); // STRING
  property.getPropertyDataFormat(); // JSON

  // Example (traversing the returned JSON)
  let result = property.getCurrentValue(entityId, entityAttributes);
  console.log(result.key) // prints the value of the key

  const property = client.getProperty('yaml-property');
  property.getPropertyDataType(); // STRING
  property.getPropertyDataFormat(); // YAML
  property.getCurrentValue(entityId, entityAttributes); // returns the stringified yaml (check above table)
```
{: codeblock}

#### Listen to the feature or property changes

To listen to the data changes, add the following code in your application:

```javascript
client.emitter.on('configurationUpdate', () => {
    // add your code
})
```
{: codeblock}
