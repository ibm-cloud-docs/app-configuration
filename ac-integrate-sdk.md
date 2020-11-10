---

copyright:
  years: 2020
lastupdated: "2020-11-10"

keywords: app-configuration, app configuration, integrate sdk, node sdk

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

{{site.data.keyword.appconfig_short}} service provides feature flags SDK, and crash insights SDKs to integrate with your Node.js microservice. 
{:shortdesc}

## Integrating feature flag SDK
{: #ac-integrate-ff-sdk}

{{site.data.keyword.appconfig_short}} service provides feature flag SDKs to integrate with your Node.js microservice application. You can evaluate the values of your feature flag by integrating the feature flag SDKs. 

1. Install the sdks using the following code from the `npm` registry.

   ```
   npm install ibm-appconfiguration-node-core --save
   npm install ibm-appconfiguration-node-feature --save
   ```
   {: codeblock}

1. In your node.js microservice, initialize the sdk with: 

   ```javascript
   const {
     AppConfigurationCore,
     UrlBuilder
   } = require('ibm-appconfiguration-node-core');

   const {
     AppConfigurationFeature
   } = require('ibm-appconfiguration-node-feature');
   ```
   {: codeblock}

1. Initialize the core sdk to connect with your App Configuration service instance.

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
   - guid: Instance Id of the App Configuration service. Get it from the service credentials section of the App Configuration service dashboard.
   - apikey: ApiKey of the App Configuration service. Get it from the service credentials section of the App Configuration service dashboard.

1. Initialize the feature flag sdk to connect with your App Configuration service instance.

   ```javascript
   const client = AppConfigurationFeature.getInstance({
     collectionId: "collection_id",
     liveFeatureUpdateEnabled: true,
     featureFile: 'custom/userJson.json'
   })
   ```
   {: codeblock}

   where,
   - collectionId: Id of the collection created in App Configuration service instance.
   - featureFile: Path to the JSON file, which contains feature details and segment details.
   - liveFeatureUpdateEnabled: Set this value to `false` if the new feature values shouldn't be fetched from the server. Make sure to provide a proper JSON file in the `featureFile` path. By default, this value is enabled.

   The AppConfigurationFeature client can be `null` if any of the configurations are invalid. In this case SDK shows the error message. To avoid errors in the app, check for `null` AppConfigurationFeature object.
   {: note}

### Set attributes
{: #ac-integrate-ff-set-attributes}

```javascript
var attributes = {
    "email":"tester@us.ibm.com",
    "creditCardExists":true,
    "name": "Tester",
    "country": "India"
  }
  client.setClientAttributes(attributes)
```
{: codeblock}

This value is used as the default attributes to evaluate the feature rules. The feature evaluation can be done by using the `request` object in the APIs also. Pass the values in `query` or `headers` to evaluate the feature rules. All these values are used during the `getCurrentValue` of the feature object.

#### Example
{: #ac-integrate-ff-example}

Request queries,

```
https://custom.server.com/api/v2/getFeature?email=tester@us.ibm.com&country=India
```

### Get single feature
{: #ac-integrate-ff-get-single-feature}

```javascript
const feature = client.getFeature('test-feature-3')

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

For feature evaluation, use the following method:

```javascript
 console.log(`Feature currentValue ${feature.getCurrentValue()} `);
```
{: codeblock}

### Get all features
{: #ac-integrate-ff-get-all-features}

```javascript
var features = client.getFeatures();

var feature = features["featureId"];

if(feature) {
    console.log(`Feature Name ${feature.getFeatureName()} `);
    console.log(`Feature ShortName ${feature.getFeatureId()} `);
    console.log(`Feature Type ${feature.getFeatureDataType()} `);
    console.log(`Feature is enabled ${feature.isEnabled()} `);
    console.log(`Feature currentValue ${feature.getCurrentValue()} `);
}
```
{: codeblock}

### Listen to the feature changes.
{: #ac-integrate-ff-listen-feature-changes}

To listen to the data changes add the following code in your application,

```javascript
  client.emitter.on('featuresUpdate', () => {
      // add your code
  })
```
{: codeblock}

## Integrating Crash SDK
{: #ac-integrate-crash-sdk}

{{site.data.keyword.appconfig_short}} service provides crash insights SDKs to integrate with your Node.js microservice application.

### Init client
{: #ac-integrate-crash-init-client}

#### Init core plug-in
{: #ac-integrate-crash-init-core-plugin}

```javascript
const { AppConfigurationCore } = require('ibm-appconfiguration-node-core');
const coreInstance = AppConfigurationCore.getInstance({
  region: 'us-south',
  guid: 'xxxxx-abc-xxxx-xxx-xxxx',
  apikey: 'abcd-xyz',
})
```
{: codeblock}

where,
- region: Region name where the service instance is created
- guid: Instance Id of the App Configuration service. Get it from the service credentials section of the dashboard.
- apikey: ApiKey of the App Configuration service. Get it from the service credentials section of the dashboard.

#### Initialize crash analytics sdk
{: #ac-integrate-crash-init-analytics-sdk}

```javascript
const { AppConfigurationCrash } = require('ibm-appconfiguration-node-crash')
const crashInstance = AppConfigurationCrash.getInstance('App Name')
```
{: codeblock}

Know more about core sdk init from [here](https://github.ibm.com/devx-app-services/apprapp-sdk-node-core)
{: note}

### Reporting Node app crashes
{: #ac-integrate-crash-report-node-crashes}

#### Crash handling by using Node process events
{: #ac-integrate-crash-handling-node-process-events}

##### Unhandled errors
{: #ac-integrate-crash-unhandled-errors}

All kinds of errors such as [Standard JavaScript errors](https://nodejs.org/api/errors.html#errors_errors), [System errors](https://nodejs.org/api/errors.html#errors_common_system_errors), and [User-specified errors](https://nodejs.org/api/errors.html#errors_class_error) triggered by application code and **did not had an exception handling** mechanism bubbles all the way back to the event loop.

Adding a handler that is shown here will listen to such uncaught exceptions and report the errors that are caught to crash sdk server.

```javascript
/* In the main file (app.js or index.js), add the following
*/
   process.on('uncaughtException', function (err) {
     crashInstance.reportCrash(err)
     process.exit(1); //recommended
   })
```
{: codeblock}

It is not safe to resume normal operations after such errors are handled. Hence, we recommend you to exit the process with a nonzero exit code `process.exit(1)`. This is to avoid infinite recursion.
{: important}

##### Unhandled promises
{: #ac-integrate-crash-unhandled-promises}

Warnings for unhandled promise rejections are deprecated. In the future, promise rejections that are not handled will terminate the Node.js process with a nonzero exit code. [See here](https://nodejs.org/api/all.html#deprecations_dep0018_unhandled_promise_rejections).
        
Whenever a promise is rejected and no error handler is attached or whose rejections have not yet been handled, crash sdk can keep track of such rejected promises.

Adding a handler that is shown here will listen to such Unhandled promise rejections and report the errors that are caught to crash sdk server.

```javascript
/* In the main file (app.js or index.js), add the following
*/
   process.on('unhandledRejection', function (err) {
     crashInstance.reportCrash(err)
   })
```
{: codeblock}

#### Node apps with Express framework
{: #ac-integrate-crash-node-apps-express-framework}

Express comes with a built-in error handler that takes care of any errors that might be encountered in the app. This default error-handling middleware function is added at the end of the middleware function stack. [See here](https://expressjs.com/en/guide/error-handling.html).

All the various kinds of errors such as [Standard JavaScript errors](https://nodejs.org/api/errors.html#errors_errors) and [User-specified errors that are triggered by application code and **did not had an exception handling** mechanism bubbles all the way back to this errorHandler middleware. 

Adding a handler that is shown here will listen and report the errors that are caught to crash sdk server.  

```javascript    
/* At the end of the middleware function stack, add the below error-handling middleware function
*/
   app.use(function (err, req, res, next) {
   crashInstance.reportCrash(err)
     // you can add your custom logic, after the crash data is reported
   })
```
{: codeblock}

Refer to Crash Handling that uses Node Process events section for handling errors that are not caught by the Express error handler middleware.
{: note}

