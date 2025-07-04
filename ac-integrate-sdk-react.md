---

copyright:
  years: 2025
lastupdated: "2025-06-12"

keywords: app-configuration, app configuration, integrate sdk, react sdk, browser, front-end

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.appconfig_short}} React client SDK
{: #ac-react}

To enhance the security of your applications using the `ibm-appconfiguration-react-client-sdk`, it is strongly recommended to use an **encrypted APIKey** instead of the plain APIKey in the init method. This change is vital to prevent exposure of sensitive credentials when users inspect your web application. If you are already using a plain APIKey, please update your application to generate and use the encrypted APIKey as per the steps mentioned [here](/docs/app-configuration?topic=app-configuration-encrypted-apikey-requirement).
{: attention}

## Overview
{: #ac-react-js-sdk-overview}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_short}} React Client SDK is used to perform feature flag and property evaluation in web applications and track custom metrics for Experimentation based on the configuration on {{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_short}} service.

{{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_short}} is a centralized feature management and configuration service
on [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/) for use with web and mobile applications, microservices, and distributed
environments.

Instrument your web applications with {{site.data.keyword.appconfig_short}} React Client SDK, and use the {{site.data.keyword.appconfig_short}} dashboard, CLI or API to define feature flags or properties, organized into collections and targeted to segments. Toggle feature flag states in the cloud to activate or deactivate features in your application or environment, when required. Run experiments and measure the effect of feature flags on end users by tracking custom metrics. You can also manage the properties for distributed applications centrally.

Compatibility : The SDK is compatible with React version 16.8.0 and higher. This SDK builds on {{site.data.keyword.appconfig_short}} JavaScript Client SDK to provide a better integration for use in React applications. As a result, much of the {{site.data.keyword.appconfig_short}} JavaScript Client SDK functionality is also available for the React Client SDK to use. Read more about {{site.data.keyword.appconfig_short}} JavaScript Client SDK [from here](https://github.com/IBM/appconfiguration-js-client-sdk#readme).
{: note}

## Integrating client SDK for React
{: #ac-integrate-react-sdk}

### Installation
{: #install-react-sdk}

Install the SDK.
```sh
npm install ibm-appconfiguration-react-client-sdk
```

### Initialize SDK
{: #initialize-react-sdk}

Initialize the sdk to connect with your {{site.data.keyword.appconfig_short}} service instance as shown in the following example. Wrapping your app component with `AppConfigProvider` lets you access features & properties from any level of your component hierarchy.

```JS
import { withAppConfigProvider } from 'ibm-appconfiguration-react-client-sdk';

(async () => {
  const AppConfigProvider = await withAppConfigProvider({
    region: 'us-south',
    guid: '<guid>',
    apikey: '<encrypted_apikey>',
    collectionId: 'airlines-webapp',
    environmentId: 'dev'
  })

  ReactDOM.render(
    <AppConfigProvider>
        <YourApp />
    </AppConfigProvider>,
    document.getElementById('root')
  );
})();
```

- region : Region name where the App Configuration service instance is created. See list of supported locations [here](https://cloud.ibm.com/catalog/services/app-configuration). Eg:- `us-south`, `au-syd` etc.
- guid : Instance Id of the {{site.data.keyword.appconfig_short}} service. Obtain it from the service credentials section of the {{site.data.keyword.appconfig_short}} dashboard.
- apikey : The encrypted APIKey generated as described [here](/docs/app-configuration?topic=app-configuration-encrypted-apikey-requirement).
- collectionId: Id of the collection created in {{site.data.keyword.appconfig_short}} service instance under the **Collections** section.
- environmentId: Id of the environment created in {{site.data.keyword.appconfig_short}} service instance under the **Environments** section.

Always use the encrypted APIKey to avoid exposing sensitive information.<br>
Ensure that you create the service credentials with the **`Client SDK`** role, as it has the minimal access permissions that are suitable to use in browser-based applications.
{: important}

### Examples for using feature and property-related APIs
{: #ac-react-example}

See the following examples for using the feature-related APIs.

#### Get single feature
{: #ac-react-get-single-feature}

```javascript
import { useFeature } from 'ibm-appconfiguration-react-client-sdk';

const feature = useFeature('featureId'); // returns undefined incase the featureId is invalid or doesn't exist

if (feature !== undefined) {
  console.log(`Feature Name ${feature.getFeatureName()} `);
  console.log(`Feature Id ${feature.getFeatureId()} `);
  console.log(`Feature Type ${feature.getFeatureDataType()} `);
  console.log(`Is feature enabled? ${feature.isEnabled()} `);
}
```
{: codeblock}

#### Get all features
{: #ac-react-get-all-features}

```javascript
import { useFeatures } from 'ibm-appconfiguration-react-client-sdk';

const features = useFeatures();
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
{: #ac-react-feature-evaluation}

You can use the `feature.getCurrentValue(entityId, entityAttributes)` method to evaluate the value of the feature flag. This method returns one of the Enabled/Disabled/Overridden value based on the evaluation. The data type of returned value matches that of feature flag. Pass a unique `entityId` as the parameter to perform the feature flag evaluation.

```javascript
const entityId = 'john_doe';
const entityAttributes = {
  city: 'Bangalore',
  country: 'India',
};

const feature = useFeature('featureId');
const featureValue = feature.getCurrentValue(entityId, entityAttributes);
```
{: codeblock}

Where:
- `entityId`: Id of the Entity. This will be a string identifier related to the Entity against which the feature is evaluated. For example, an entity might be an instance of an app that runs on a mobile device, or a user accessing the web application. For any entity to interact with {{site.data.keyword.appconfig_short}}, it must provide a unique entity ID.
- `entityAttributes`: A JSON object consisting of the attribute name and their values that defines the specified entity. This is an optional parameter if the feature flag is not configured with any targeting definition. If the targeting is configured, then entityAttributes should be provided for the rule evaluation. An attribute is a parameter that is used to define a segment. The SDK uses the attribute values to determine if the specified entity satisfies the targeting rules, and returns the appropriate feature flag value.

#### Send custom metrics

Record custom metrics using the `useTrack` hook in experimentation.

```javascript
import { useTrack } from 'ibm-appconfiguration-react-client-sdk';

export default MyComponent = function () {
    const trackEvent = useTrack();
    return (
        <button onClick={() => trackEvent('clicked', 'user123')}>Buy</button>
    )
}
```

#### Get single property
{: #ac-react-get-single-property}

```javascript
import { useProperty } from 'ibm-appconfiguration-react-client-sdk';

const property = useProperty('propertyId'); // returns undefined incase the propertyId is invalid or doesn't exist

if (property !== undefined) {
  console.log(`Property Name ${property.getPropertyName()} `);
  console.log(`Property Id ${property.getPropertyId()} `);
  console.log(`Property Type ${property.getPropertyDataType()} `);
}
```
{: codeblock}

#### Get all properties
{: #ac-react-get-all-properties}

```javascript
import { useProperties } from 'ibm-appconfiguration-react-client-sdk';

const properties = useProperties();
const property = properties['propertyId'];

if (property !== undefined) {
  console.log(`Property Name ${property.getPropertyName()} `);
  console.log(`Property Id ${property.getPropertyId()} `);
  console.log(`Property Type ${property.getPropertyDataType()} `);
}
```
{: codeblock}

#### Evaluate a property
{: #ac-react-property-evaluation}

Use the `property.getCurrentValue(entityId, entityAttributes)` method to evaluate the value of the property. This method returns the default property value or its overridden value based on the evaluation. The data type of returned value matches that of property.

```javascript
const entityId = 'john_doe';
const entityAttributes = {
  city: 'Bangalore',
  country: 'India',
};

const property = useProperty('propertyId');
const propertyValue = property.getCurrentValue(entityId, entityAttributes);
```
{: codeblock}

Where:
- `entityId`: Id of the Entity. This will be a string identifier related to the Entity against which the property is evaluated. For any entity to interact with {{site.data.keyword.appconfig_short}}, it must provide a unique entity ID.
- `entityAttributes`: A JSON object consisting of the attribute name and their values that defines the specified entity. This is an optional parameter if the property is not configured with any targeting definition. If the targeting is configured, then entityAttributes should be provided for the rule evaluation. An attribute is a parameter that is used to define a segment. The SDK uses the attribute values to determine if the specified entity satisfies the targeting rules, and returns the appropriate property value.

#### Using fallback values with the React Client SDK

In case of a connection error with the {{site.data.keyword.appconfig_short}}, the SDK relies on the most recently assessed flag values retained in memory. However, if no prior values exist in memory, it's advisable for users to establish fallback values within their code, ensuring smooth operation. An example showcasing this fallback approach is provided by the following example.

```javascript

import { useFeatures } from 'ibm-appconfiguration-react-client-sdk';

export default function App {
  const features = useFeatures();
  const defaultFlagValues = {
    'flight-booking': false
  }
  const entityId = 'john_doe';
  const entityAttributes = {
    city: 'Bangalore',
    country: 'India',
  };

  const getAppConfigurationFlags = (featureID, features) => {
    if (Object.keys(features).length === 0 && features.constructor === Object) {
      return defaultFlagValues[featureID];
    }

    return feature[featureID]
      ? feature[featureID].getCurrentValue(entityId, entityAttributes)
      : defaultFlagValues[featureID];
  };

  return getAppConfigurationFlags('flight-booking', features) ? <div>Flight Booking</div> : '';
}
```

### Supported Data types
{: #ac-react-supported-data-types}

{{site.data.keyword.appconfig_short}} service allows to configure the feature flag and properties in the following data types : Boolean,
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
const feature = useFeature('json-feature');
feature.getFeatureDataType(); // STRING
feature.getFeatureDataFormat(); // JSON

// Example (traversing the returned JSON)
let result = feature.getCurrentValue(entityId, entityAttributes);
console.log(result.key) // prints the value of the key

const feature = useFeature('yaml-feature');
feature.getFeatureDataType(); // STRING
feature.getFeatureDataFormat(); // YAML
feature.getCurrentValue(entityId, entityAttributes); // returns the stringified yaml (check above table)
```
{: codeblock}

</details>
<details><summary>Property usage example</summary>

```javascript
const property = useProperty('json-property');
property.getPropertyDataType(); // STRING
property.getPropertyDataFormat(); // JSON

// Example (traversing the returned JSON)
let result = property.getCurrentValue(entityId, entityAttributes);
console.log(result.key) // prints the value of the key

const property = useProperty('yaml-property');
property.getPropertyDataType(); // STRING
property.getPropertyDataFormat(); // YAML
property.getCurrentValue(entityId, entityAttributes); // returns the stringified yaml (check above table)
```
{: codeblock}

</details>

### License
{: #apache-react-license}

This project is released under the Apache 2.0 license. The license's full text can be found
in [LICENSE](https://github.com/IBM/appconfiguration-react-client-sdk/blob/main/LICENSE)

### Listen to the feature or property changes
{: #ac-react-feature-prop-change}

The SDK automatically subscribes to event-based mechanism and re-renders the enclosed components when feature flag's or property's configuration changes.
