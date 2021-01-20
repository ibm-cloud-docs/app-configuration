---

copyright:
  years: 2020, 2021
lastupdated: "2021-01-18"

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

{{site.data.keyword.appconfig_short}} service provides feature flags SDK, and crash insights SDK to integrate with your Node.js microservice or application. 
{:shortdesc}

## Integrating {{site.data.keyword.appconfig_short}} SDK
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

### Examples for using feature related APIs
{: #ac-integrate-ff-example}

Refer to the below examples for using the feature related APIs.

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

## Integrating Crash SDK
{: #ac-integrate-crash-sdk}

{{site.data.keyword.appconfig_short}} service provides crash insights SDK to integrate with your Node.js microservice. You can monitor and analyze the crashes and errors encountered in your application in the {{site.data.keyword.appconfig_short}} service dashboard by integrating the crash SDK.

1. Install the sdks using the following code from the `npm` registry or add these packages as dependencies in the `package.json` file .

   ```
   npm install ibm-appconfiguration-node-core --save
   npm install ibm-appconfiguration-node-crash --save
   ```
   {: codeblock}

1. In your node.js microservice, include the sdk module with: 

   ```javascript
   const {
     AppConfigurationCore
   } = require('ibm-appconfiguration-node-core');
   
   const {
     AppConfigurationCrash
   } = require('ibm-appconfiguration-node-crash');
   ```
   {: codeblock}

1. Initialize the core sdk to connect with your {{site.data.keyword.appconfig_short}} service instance. You may skip this step if you already initialized the core SDK while integrating feature flag SDK.

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

1. Initialize the crash sdk to connect with your {{site.data.keyword.appconfig_short}} service instance.

   ```javascript
   const { AppConfigurationCrash } = require('ibm-appconfiguration-node-crash')
   const crashInstance = AppConfigurationCrash.getInstance('App Name')
   ```
   {: codeblock}

   where, `appName` is the name of your application.

### Reporting Node app crashes
{: #ac-integrate-crash-report-node-crashes}

#### Crash handling by using Node process events
{: #ac-integrate-crash-handling-node-process-events}

##### Unhandled errors
{: #ac-integrate-crash-unhandled-errors}

All kinds of errors such as [Standard JavaScript errors](https://nodejs.org/api/errors.html#errors_errors){: external}, [System errors](https://nodejs.org/api/errors.html#errors_common_system_errors){: external}, and [User-specified errors](https://nodejs.org/api/errors.html#errors_class_error){: external} are triggered by application code and did not have an exception handling mechanism, bubbles all the way up to the event loop.

Adding a handler that is shown here will listen to such uncaught exceptions and report the errors to the {{site.data.keyword.appconfig_short}} service.

```javascript
/* 
In the main file (app.js or index.js), add the following
*/
   process.on('uncaughtException', function (err) {
     crashInstance.reportCrash(err)
     process.exit(1); //recommended
   })
```
{: codeblock}

##### Unhandled promises
{: #ac-integrate-crash-unhandled-promises}

Warnings for unhandled promise rejections are deprecated. In the future, promise rejections that are not handled will terminate the Node.js process with a nonzero exit code. [See here](https://nodejs.org/api/all.html#deprecations_dep0018_unhandled_promise_rejections){: external}.
        
Whenever a promise is rejected and no error handler is attached or whose rejections have not yet been handled, crash SDK can keep track of such rejected promises.

Adding a handler that is shown here will listen to Unhandled promise rejections and report the errors to the {{site.data.keyword.appconfig_short}} service.

```javascript
/* 
In the main file (app.js or index.js), add the following
*/
   process.on('unhandledRejection', function (err) {
     crashInstance.reportCrash(err)
   })
```
{: codeblock}

#### Node apps with Express framework
{: #ac-integrate-crash-node-apps-express-framework}

Express comes with a built-in error handler that takes care of any errors that might be encountered in the app. This default error-handling middleware function is added at the end of the middleware function stack. [See here](https://expressjs.com/en/guide/error-handling.html){: external}.

All the various kinds of errors such as [Standard JavaScript errors](https://nodejs.org/api/errors.html#errors_errors){: external} and [User-specified errors](https://nodejs.org/api/errors.html#errors_class_error){: external} that are triggered by application code and did not had an exception handling mechanism bubbles all the way up to this errorHandler middleware. 

Adding a handler that is shown here will listen and report the errors to the {{site.data.keyword.appconfig_short}} service.  

```javascript    
/* 
At the end of the middleware function stack, add the below error-handling middleware function
*/
   app.use(function (err, req, res, next) {
   crashInstance.reportCrash(err)
     // you can add your custom logic, after the crash data is reported
   })
```
{: codeblock}

