---

copyright:
  years: 2020, 2021
lastupdated: "2021-01-12"

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

# Integrate {{site.data.keyword.appconfig_short}} service SDKs
{: #ac-integrate-sdks}

{{site.data.keyword.appconfig_short}} service provides feature flags SDK to integrate with your Node.js microservice or application. 
{:shortdesc}

## Integrating feature flag SDK
{: #ac-integrate-ff-sdk}

{{site.data.keyword.appconfig_short}} service provides feature flag SDK to integrate with your Node.js microservice or application. You can evaluate the values of your feature flag by integrating the feature flag SDK. 

1. Install the SDK using the following code from the `npm` registry or add these packages as dependencies in the `package.json` file.

   ```
   npm install ibm-appconfiguration-node-core --save
   npm install ibm-appconfiguration-node-feature --save
   ```
   {: codeblock}

1. In your Node.js microservice, include the SDK module with: 

   ```javascript
   const {
     AppConfigurationCore
   } = require('ibm-appconfiguration-node-core');
   
   const {
     AppConfigurationFeature
   } = require('ibm-appconfiguration-node-feature');
   ```
   {: codeblock}

1. Initialize the core sdk to connect with your {{site.data.keyword.appconfig_short}} service instance.

   ```javascript
   const coreClient = AppConfigurationCore.getInstance({
       region: 'us-south',
       guid: '6fcXXXX-XXX-4cd9-XXX-fXXXXXXX00',
       apikey: 'abcd',
     })
   ```
   {: codeblock}

   where,
   - region: Region name where the service instance is created. Use `us-south` for Dallas and `eu-gb` for London.
   - guid: Instance Id of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - apikey: ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.

1. Initialize the feature flag SDK to connect with your {{site.data.keyword.appconfig_short}} service instance.

   ```javascript
   const featureClient = AppConfigurationFeature.getInstance({
     collectionId: "collection_id",
     liveFeatureUpdateEnabled: true,
     featureFile: 'custom/userJson.json'
   })
   ```
   {: codeblock}

   where,
   - collectionId: Id of the collection created in {{site.data.keyword.appconfig_short}} service instance.
   - liveFeatureUpdateEnabled: Set this value to `false` if the new feature values shouldn't be fetched from the server. Make sure to provide a proper JSON file in the `featureFile` path. By default, this value is enabled.
   - featureFile: Path to the JSON file, which contains feature details and segment details.

   The `AppConfigurationFeature` client can be `null` if any of the configurations are invalid. In this case SDK shows the error message. To avoid errors in the app, check for `null` AppConfigurationFeature object.
   {: note}

1. Set attributes: You can set the attributes values that define the segments using `setClientAttributes` method. This value is used as the default attributes to evaluate the feature rules. 
{: #set-attributes}

   ```javascript
   var attributes = {
       "city":"Bengaluru",
       "country": "India"
     }
     featureClient.setClientAttributes(attributes)   
   ```
   {: codeblock}

   The feature evaluation can also be done by using the `request` object in the APIs. Pass the values in `query` or `headers` or `body` to evaluate the feature rules. All these values are used during the `getCurrentValue` of the feature object.

   For example, you can pass the attributes as part of the headers in the request to your API as below:

   ```
   curl --request GET 'https://customerapiserver.com/api/v2/getAppData' --header 'city: Bengaluru' --header 'country: India'
   ```
   {: codeblock}

### Examples
{: #ac-integrate-ff-example}

Refer to the below examples for using the feature related APIs.

#### Get all features
{: #ac-integrate-ff-get-all-features}

```javascript
var features = featureClient.getFeatures();

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

#### Get single feature
{: #ac-integrate-ff-get-single-feature}

```javascript
const feature = featureClient.getFeature('feature_Id')

if(feature) {

    if(feature.isEnabled()) {
        // enable feature
    } else {
        // disable the feature
    }
    console.log("data", feature);
    console.log(`\n Feature Name ${feature.getFeatureName()} `);
    console.log(`Feature ShortName ${feature.getFeatureId()} `);
    console.log(`Feature Type ${feature.getFeatureDataType()} `);
    console.log(`Feature is enabled ${feature.isEnabled()} `);
    console.log(`Feature currentValue ${feature.getCurrentValue()} `);
}
```
{: codeblock}

The AppConfigurationFeature getFeature can be `null` if the featureId is invalid. In this case SDK shows the error message. To avoid errors in the app, check for `null` AppConfigurationFeature getFeature.
{: note}

#### Feature evaluation
{: #ac-integrate-ff-feature-evaluation}

You can use the `feature.getCurrentValue()` method to evaluate the value of the feature flag. If the feature flag is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values used for evaluation using one of the below methods:

- Feature evaluation using the attributes set in `Client Attributes`. Refer to [Set Attributes](#set-attributes) for more details. 

   ```javascript
   console.log(`Feature currentValue ${feature.getCurrentValue()} `);
   ```
   {: codeblock}

- Feature evaluation using the `Request` object. Pass the request object, to use the attributes set in request headers, body and query parameters for feature evaluation.

   ```javascript
   app.get('/', function (req, res) {

     ........
     console.log(`Feature currentValue with req object :  ${feature.getCurrentValue(req)}`)
     .....

   })
   ```
   {: codeblock}

#### Listen to the feature changes
{: #ac-integrate-ff-listen-feature-changes}

To listen to the data changes add the following code in your application

```javascript
  featureClient.emitter.on('featuresUpdate', () => {
      // add your code
  })
```
{: codeblock}

