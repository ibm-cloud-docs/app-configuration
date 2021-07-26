---

copyright:
  years: 2020, 2021
lastupdated: "2021-07-19"

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
{:shortdesc}

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

1. *Optional*: You can work [offline](/docs/app-configuration?topic=app-configuration-ac-offline) with local feature file and perform [feature operations](#ac-integrate-ff-example).
   {: #ac-work-offline-ff}

   After `client.init(region, guid, apikey)`:

   ```javascript
   let configurationFile = 'path/to/configuration/file.json';
   let liveConfigUpdateEnabled = false;
   client.setContext(collectionId, environmentId, configurationFile, liveConfigUpdateEnabled)
   ```
   {: codeblock}

   where,
   - configurationFile: Path to the JSON file, which contains configuration details.
   - liveConfigUpdateEnabled: Set this value to false if the new configuration values shouldn't be fetched from the server. Make sure to provide a proper JSON file in the path. By default, liveConfigUpdateEnabled value is enabled.


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
var features = client.getFeatures();

var feature = features["feature_id"];

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
   let entityId = 'entityId'
   let entityAttributes = {
       'city': 'Bangalore',
       'country': 'India'
   }

   feature.getCurrentValue(entityId, entityAttributes)
   ```
   {: codeblock}

* If the feature flag is not targeted to any segments and the feature flag is turned **ON** this method returns the feature **enabled value**. And when the feature flag is turned **OFF** this method returns the feature **disabled value**.

   ```javascript
   let entityId = 'entityId'
   feature.getCurrentValue(entityId)
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
var properties = client.getProperties();

var property = properties["property_id"];

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
   let entityId = 'entityId'
   let entityAttributes = {
       'city': 'Bangalore',
       'country': 'India'
   }

   property.getCurrentValue(entityId, entityAttributes)    
   ```
   {: codeblock}

- If the property is not targeted to any segments, this method returns the property value.

   ```javascript
   let entityId = 'entityId'
   property.getCurrentValue(entityId)
   ```
   {: codeblock}

#### Listen to the feature or property changes
{: #ac-integrate-ff-listen-feature-changes}

To listen to the data changes, add the following code in your application:

```javascript
client.emitter.on('configurationUpdate', () => {
    // add your code
})
```
{: codeblock}
