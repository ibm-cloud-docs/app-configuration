---

copyright:
  years: 2022, 2025
lastupdated: "2025-06-12"

keywords: app-configuration, app configuration, integrate sdk, javascript sdk, browser, front-end

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# App Configuration JavaScript client SDK
{: #ac-javascript}

To enhance the security of your applications using the `ibm-appconfiguration-js-client-sdk`, it is strongly recommended to use an **encrypted APIKey** instead of the plain APIKey in the init method. This change is vital to prevent exposure of sensitive credentials when users inspect your web application. If you are already using a plain APIKey, please update your application to generate and use the encrypted APIKey as per the steps mentioned [here](/docs/app-configuration?topic=app-configuration-encrypted-apikey-requirement).
{: attention}

## Overview
{: #ac-js-sdk-overview}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_short}} JavaScript Client SDK is used to perform feature flag and property evaluation in web applications and track custom metrics for Experimentation based on the configuration on {{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_short}} service.

{{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_short}} is a centralized feature management and configuration service
on [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/) for use with web and mobile applications, microservices, and distributed
environments.

Instrument your web applications with {{site.data.keyword.appconfig_short}} JavaScript Client SDK, and use the {{site.data.keyword.appconfig_short}} dashboard, CLI or API to define feature flags or properties, organized into collections and targeted to segments. Toggle feature flag states in
the cloud to activate or deactivate features in your application or environment, when required. Run experiments and measure the effect of feature flags on end users by tracking custom metrics. You can also manage the properties for distributed applications centrally.

Browser Compatibility: The SDK is supported on all major browsers. The Browser should have `fetch()` API support.
{: note}

## Integrating client SDK for JavaScript
{: #ac-integrate-js-sdk}

### Installation
{: #install-js-sdk}

Install the SDK. Use the following code to install as a module from package manager.

```sh
npm install ibm-appconfiguration-js-client-sdk
```
You can import the SDK into the script tag either by referencing it from a hosted site on your backend or from a CDN as follows:

Example:
```html
<script type="text/javascript" src="https://unpkg.com/ibm-appconfiguration-js-client-sdk/dist/appconfiguration.js"></script>
```

### Initialize SDK
{: #initialize-js-sdk}

Initialize the sdk to connect with your {{site.data.keyword.appconfig_short}} service instance.

```JS
const region = AppConfiguration.REGION_US_SOUTH;
const guid = '<guid>';
const apikey = '<encrypted_apikey>';

const collectionId = 'airlines-webapp';
const environmentId = 'dev';

const appConfigClient = AppConfiguration.getInstance();

async function initialiseAppConfig() {
    appConfigClient.init(region, guid, apikey);
    await appConfigClient.setContext(collectionId, environmentId);
}

try {
    await initialiseAppConfig();
    console.log("app configuration sdk init successful");
} catch (e) {
    console.error("failed to initialise app configuration sdk", e);
}
```

In the previous snippet, the async function `initialiseAppConfig()` will return an `Promise<void>` that resolves when the configurations are successfully fetched. Else, throws error if unsuccessful.

 It is expected that initialisation to be done **only once**.
 {: important}

After the SDK is initialised successfully the feature flag & properties can be retrieved using the `appConfigClient` as shown in the following code snippet.
<details><summary>Expand to view the example snippet</summary>

```js
// other-file.js
const appConfigClient = AppConfiguration.getInstance();

const feature = appConfigClient.getFeature('online-check-in');
const result = feature.getCurrentValue(entityId, entityAttributes);
console.log(result);

const property = appConfigClient.getProperty('check-in-charges');
const result = property.getCurrentValue(entityId, entityAttributes);
console.log(result);
```
</details>

where,
- **region** : Region name where the App Configuration service instance is created. See list of supported locations [here](https://cloud.ibm.com/catalog/services/app-configuration). Eg:- `us-south`, `au-syd` etc.
- **guid** : Instance ID of the {{site.data.keyword.appconfig_short}} service. Obtain it from the service credentials section of the {{site.data.keyword.appconfig_short}} dashboard.
- **apikey** : The encrypted APIKey generated as described [here](/docs/app-configuration?topic=app-configuration-encrypted-apikey-requirement).
- **collectionId**: ID of the collection created in App Configuration service instance under the **Collections** section.
- **environmentId**: ID of the environment created in App Configuration service instance under the **Environments** section.

Always use the encrypted APIKey to avoid exposing sensitive information.<br>
Ensure that you create the service credentials with the **`Client SDK`** role, as it has the minimal access permissions that are suitable to use in browser-based applications.
{: important}

### Examples for using feature and property-related APIs
{: #ac-js-example}

See the following examples for using the feature-related APIs.

#### Get single feature
{: #ac-js-get-single-feature}

```javascript
const feature = appConfigClient.getFeature('featureId'); // throws error incase the featureId is invalid or doesn't exist
console.log(`Feature Name ${feature.getFeatureName()} `);
console.log(`Feature Id ${feature.getFeatureId()} `);
console.log(`Feature Type ${feature.getFeatureDataType()} `);
```
{: codeblock}

#### Get all features
{: #ac-js-get-all-features}

```javascript
const features = appConfigClient.getFeatures();
const feature = features['featureId'];

if (feature !== undefined) {
  console.log(`Feature Name ${feature.getFeatureName()} `);
  console.log(`Feature Id ${feature.getFeatureId()} `);
  console.log(`Feature Type ${feature.getFeatureDataType()} `);
  console.log(`Is feature enabled? ${feature.isEnabled()} `);
}
```
{: codeblock}

#### Evaluate a feature
{: #ac-js-feature-evaluation}

Use the `feature.getCurrentValue(entityId, entityAttributes)` method to evaluate the value of the feature flag.
This method returns one of the Enabled/Disabled/Overridden value based on the evaluation. The data type of returned value matches that of feature flag.

```javascript
const entityId = 'john_doe';
const entityAttributes = {
  city: 'Bangalore',
  country: 'India',
};

const feature = appConfigClient.getFeature('featureId');
const featureValue = feature.getCurrentValue(entityId, entityAttributes);
```
{: codeblock}

- `entityId`: Id of the Entity. This will be a string identifier related to the Entity against which the feature is evaluated. For example, an entity might be an instance of an app that runs on a mobile device, or a user accessing the web application. For any entity to interact with App Configuration, it must provide a unique entity ID.
- `entityAttributes`: A JSON object consisting of the attribute name and their values that defines the specified entity. This is an optional parameter if the feature flag is not configured with any targeting definition. If the targeting is configured, then entityAttributes should be provided for the rule evaluation. An attribute is a parameter that is used to define a segment. The SDK uses the attribute values to determine if the specified entity satisfies the targeting rules, and returns the appropriate feature flag value.

#### Send custom metrics
{: #send-custom-metrics-js}

Record custom metrics to use in experimentation using the track function.

```javascript
appConfigClient.track(eventKey, entityId)
```
where
- `eventKey`: The event key for the metric associated with the running experiment. The event key in your metric and the event key in your code must match exactly.

#### Get single property
{: #ac-js-get-single-property}

```javascript
const property = appConfigClient.getProperty('propertyId'); // throws error incase the propertyId is invalid or doesn't exist
console.log(`Property Name ${property.getPropertyName()} `);
console.log(`Property Id ${property.getPropertyId()} `);
console.log(`Property Type ${property.getPropertyDataType()} `);
```
{: codeblock}

#### Get all properties
{: #ac-js-get-all-properties}

```javascript
const properties = appConfigClient.getProperties();
const property = properties['propertyId'];

if (property !== undefined) {
  console.log(`Property Name ${property.getPropertyName()} `);
  console.log(`Property Id ${property.getPropertyId()} `);
  console.log(`Property Type ${property.getPropertyDataType()} `);
}
```
{: codeblock}

#### Evaluate a property
{: #ac-js-property-evaluation}

Use the `property.getCurrentValue(entityId, entityAttributes)` method to evaluate the value of the property.
This method returns the default property value or its overridden value based on the evaluation. The data type of returned value matches that of property.

```javascript
const entityId = 'john_doe';
const entityAttributes = {
  city: 'Bangalore',
  country: 'India',
};

const property = appConfigClient.getProperty('propertyId');
const propertyValue = property.getCurrentValue(entityId, entityAttributes);
```
{: codeblock}

- `entityId`: Id of the Entity. This will be a string identifier related to the Entity against which the property is evaluated. For example, an entity might be an instance of an app that runs on a mobile device, or a user accessing the web application. For any entity to interact with App Configuration, it must provide a unique entity ID.
- `entityAttributes`: A JSON object consisting of the attribute name and their values that defines the specified entity. This is an optional parameter if the property is not configured with any targeting definition. If the targeting is configured, then entityAttributes should be provided for the rule evaluation. An attribute is a parameter that is used to define a segment. The SDK uses the attribute values to determine if the specified entity satisfies the targeting rules, and returns the appropriate property value.

### Logging
{: #ac-js-logging}

Set the logging level to one of 'debug' | 'info' | 'warning' | 'error'. The default logging level is `info`.

```javascript
appConfigClient.setLogLevel('debug');
```

### Supported Data types
{: #supported-data-types}

App Configuration service allows to configure the feature flag and properties in the following data types : Boolean,
Numeric, String. The String data type can be of the format of a text string , JSON or YAML. The SDK processes each
format accordingly as shown in the following table.

<details><summary>View Table</summary>

| **Feature or Property value**                                                                          | **DataType** | **DataFormat** | **Type of data returned <br> by `getCurrentValue()`** | **Example output**                                                                   |
| ------------------------------------------------------------------------------------------------------ | ------------ | -------------- | ----------------------------------------------------- | ------------------------------------------------------------------------------------ |
| `true`                                                                                                 | BOOLEAN      | not applicable | `boolean`                                             | `true`                                                                               |
| `25`                                                                                                   | NUMERIC      | not applicable | `number`                                              | `25`                                                                                 |
| "a string text"                                                                                        | STRING       | TEXT           | `string`                                              | `a string text`                                                                      |
| <pre>{<br>  "firefox": {<br>    "name": "Firefox",<br>    "pref_url": "about:config"<br>  }<br>}</pre> | STRING       | JSON           | `JSON object`                                         | `{"firefox":{"name":"Firefox","pref_url":"about:config"}}`                           |
| <pre>men:<br>  - John Smith<br>  - Bill Jones<br>women:<br>  - Mary Smith<br>  - Susan Williams</pre>  | STRING       | YAML           | `string`                                              | `"men:\n  - John Smith\n  - Bill Jones\nwomen:\n  - Mary Smith\n  - Susan Williams"` |
</details>

<details><summary>Feature flag usage Example</summary>

```javascript
const feature = appConfigClient.getFeature('json-feature');
feature.getFeatureDataType(); // STRING
feature.getFeatureDataFormat(); // JSON

// Example (traversing the returned JSON)
let result = feature.getCurrentValue(entityId, entityAttributes);
console.log(result.key) // prints the value of the key

const feature = appConfigClient.getFeature('yaml-feature');
feature.getFeatureDataType(); // STRING
feature.getFeatureDataFormat(); // YAML
feature.getCurrentValue(entityId, entityAttributes); // returns the stringified yaml (check the table)
```
{: codeblock}

</details>
<details><summary>Property usage example</summary>

```javascript
const property = appConfigClient.getProperty('json-property');
property.getPropertyDataType(); // STRING
property.getPropertyDataFormat(); // JSON

// Example (traversing the returned JSON)
let result = property.getCurrentValue(entityId, entityAttributes);
console.log(result.key) // prints the value of the key

const property = appConfigClient.getProperty('yaml-property');
property.getPropertyDataType(); // STRING
property.getPropertyDataFormat(); // YAML
property.getCurrentValue(entityId, entityAttributes); // returns the stringified yaml (check the table)
```
{: codeblock}

</details>

### Set listener for feature and property data changes

The SDK provides an event-based mechanism to notify you in real-time when feature flag's or property's configuration changes. You can listen to `configurationUpdate` event using the same appConfigClient.

```javascript
appConfigClient.emitter.on('configurationUpdate', () => {
  // **add your code**
  // To find the effect of any configuration changes, you can call the feature or property related methods

  // feature = appConfigClient.getFeature('online-check-in');
  // newValue = feature.getCurrentValue(entityId, entityAttributes);
});
```

### Examples
{: #evaluation-examples}

Try [this](https://github.com/IBM/appconfiguration-js-client-sdk/tree/main/example) sample application in the examples
folder to learn more about feature and property evaluation.

### License
{: #apache-js-license}

This project is released under the Apache 2.0 license. The license's full text can be found
in [LICENSE](https://github.com/IBM/appconfiguration-js-client-sdk/blob/main/LICENSE)
