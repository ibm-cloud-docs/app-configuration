---

copyright:
  years: 2020, 2021
lastupdated: "2021-02-02"

keywords: app-configuration, app configuration, integrate sdk, core sdk, node sdk, npm

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

# App Configuration service SDK for Node
{: #ac-integrate-sdks}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Node.js microservice or application. 
{:shortdesc}

## Integrating {{site.data.keyword.appconfig_short}} SDK
{: #ac-integrate-ff-sdk}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Node.js microservice or application. You can evaluate the values of your feature flag by integrating the {{site.data.keyword.appconfig_short}} SDK. 

1. Install the SDK using the following code from the `npm` registry or add these packages as dependencies in the `package.json` file.

   ```
   npm install ibm-appconfiguration-node-sdk
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

   ```javascript
   const client = AppConfiguration.getInstance();

   let region = 'us-south';
   let guid = 'abc-def-xyz';
   let apikey = 'j9qc-abc-z79';

   client.init(region, guid, apikey)

   // Initialize feature
   client.setCollectionId('collectionId')
   ```
   {: codeblock}

   where,
   - region: Region name where the service instance is created. Use `us-south` for Dallas and `eu-gb` for London.
   - guid: Instance Id of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - apikey: ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - collectionId: Id of the collection created in {{site.data.keyword.appconfig_short}} service instance.

   The `AppConfiguration` client can be `null` if any of the configurations in `init()` and `setCollectionId()` are missing or invalid. In this case, the SDK shows the error message. To avoid errors in the app, check for `null` AppConfiguration object.
   {: note}

1. *Optional*: You can work offline with local feature file and perform [feature operations](#ac-integrate-ff-example).

   ```javascript
   client.setCollectionId('collectionId')
   client.fetchFeaturesFromFile(liveFeatureUpdateEnabled, featureFile='path/to/feature/file.json')
   ```
   {: codeblock}

   where,
   - liveFeatureUpdateEnabled: Set this value to `false` if the new feature values shouldn't be fetched from the server. Make sure to provide a proper JSON file in the `featureFile` path. By default, this value is enabled.
   - featureFile: Path to the JSON file, which contains feature details and segment details.

   The `AppConfiguration` client can be `null` if any of the configurations are invalid. In this case, the SDK shows the error message. To avoid errors in the app, check for `null` AppConfiguration object.
   {: note}

1. Set identity: You can set the attributes values that define the segments using `setIdentity()` method. The identity object contains the identifier and the attributes. `setIdentity()` is to be set mandatorily. This value is used as the default attributes to evaluate the feature rules. 
{: #set-attributes}

   ```javascript
   var identity = {
       "id":"pvQ213",
       "city": "Bangalore",
   }
   client.setIdentity(identity)
   ```
   {: codeblock}

   Use the updateIdentity() method, as shown below for updating the indentity.
   ```javascript
   var identity = {
       "city": "Chennai",
   }
   client.updateIdentity(identity)
   ```
   {: codeblock}
   {: note}

### Examples for using feature related APIs
{: #ac-integrate-ff-example}

Refer to the below examples for using the feature related APIs.

#### Get single feature
{: #ac-integrate-ff-get-single-feature}

```javascript
const feature = client.getFeature('feature_Id')

if(feature) {

   if(feature.isEnabled()) {
       // enable feature
   } else {
      // disable the feature
   }
   console.log('data', feature);
   console.log(`Feature Name ${feature.getFeatureName()} `);
   console.log(`Feature ShortName ${feature.getFeatureId()} `);
   console.log(`Feature Type ${feature.getFeatureDataType()} `);
   console.log(`Feature is enabled ${feature.isEnabled()} `);
   console.log(`Feature currentValue ${feature.getCurrentValue()} `);
}
```
{: codeblock}

The AppConfiguration getFeature can be `null` if the `feature_Id` is invalid. In this case, the SDK shows the error message. To avoid errors in the app, check for `null` AppConfiguration getFeature.
{: note}

#### Get all features
{: #ac-integrate-ff-get-all-features}

```javascript
var features = client.getFeatures();

var feature = features["feature_Id"];

if(feature) {
    console.log(`Feature Name ${feature.getFeatureName()} `);
    console.log(`Feature ShortName ${feature.getFeatureId()} `);
    console.log(`Feature Type ${feature.getFeatureDataType()} `);
    console.log(`Feature is enabled ${feature.isEnabled()} `);
    console.log(`Feature currentValue ${feature.getCurrentValue()} `);
}
```
{: codeblock}

#### Feature evaluation
{: #ac-integrate-ff-feature-evaluation}

You can use the `feature.getCurrentValue()` method to evaluate the value of the feature flag. If the feature flag is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values using the [identity object](#set-attributes).

```javascript
console.log(`Feature currentValue ${feature.getCurrentValue()} `);
```
{: codeblock}

#### Listen to the feature changes
{: #ac-integrate-ff-listen-feature-changes}

To listen to the data changes, add the following code in your application:

```javascript
client.emitter.on('featuresUpdate', () => {
    // add your code
})
```
{: codeblock}

