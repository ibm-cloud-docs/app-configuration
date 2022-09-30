---

copyright:
  years: 2022
lastupdated: "2022-09-30"

keywords: app-configuration, app configuration, integrate sdk, javascript sdk, browser, front-end

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# App Configuration JavaScript client SDK
{: #ac-javascript}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your browser applications.
{: shortdesc}

## Integrating client SDK for JavaScript
{: #ac-integrate-js-sdk}

{{site.data.keyword.appconfig_short}} JavaScript client SDK can be used with all the major browsers. You can evaluate the values of your feature flag and property by integrating the {{site.data.keyword.appconfig_short}} SDK.

1. Install the SDK. Use the following code to install the SDK as a module from package manager.

   ```bash
   npm install ibm-appconfiguration-js-client-sdk
   ```
   {: codeblock}

1. You can import the SDK into the `script` tag either by referencing it from a hosted site on your backend or from a CDN as follows:

   ```javascript
   <script type="text/javascript" src="https://unpkg.com/ibm-appconfiguration-js-client-sdk@latest/dist/appconfiguration.js"></script>
   ```
   {: codeblock}

1. Initialize the sdk to connect with your {{site.data.keyword.appconfig_short}} service instance.
   {: #ac-init-js-sdk}

   ```javascript
   const region = AppConfiguration.REGION_US_SOUTH;
   const guid = '<guid>';
   const apikey = '<apikey>';
   const collectionId = '<collectionId>';
   const environmentId = '<environmentId>';

   const client = AppConfiguration.getInstance();
   client.init(region, guid, apikey);
   await client.setContext(collectionId, environmentId);
   ```
   {: codeblock}

   The `init()` and `setContext()` are the initialisation methods and should be invoked only once using appConfigClient. The appConfigClient, once initialised, can be obtained across modules using `AppConfiguration.getInstance()`.

   Where:
   - `region`: Region where the service instance is created. Use `AppConfiguration.REGION_US_SOUTH` for Dallas, `AppConfiguration.REGION_US_EAST` for Washington DC, `AppConfiguration.REGION_EU_GB` for London, and `AppConfiguration.REGION_AU_SYD` for Sydney.
   - `guid`: Instance ID of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - `apikey`: API key of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - `collectionId`: ID of the collection created in App Configuration service instance under the Collections section.
   - `environmentId`: ID of the environment created in App Configuration service instance under the Environments section.

Ensure to create the service credentials of the role `Client SDK` for using with the JavaScript SDK. API key of the `Client SDK` role has minimal access permissions that are suitable to use in browser based applications.
{: note}

### Examples for using feature and property-related APIs
{: #ac-js-example}

See the following examples for using the feature-related APIs.

#### Get single feature
{: #ac-js-get-single-feature}

```javascript
const feature = client.getFeature('feature_id')

if(feature) {

   console.log('data', feature);
   console.log(`Feature Name ${feature.getFeatureName()} `);
   console.log(`Feature Id ${feature.getFeatureId()} `);
   console.log(`Feature Type ${feature.getFeatureDataType()} `);
   console.log(`Feature is enabled ${feature.isEnabled()} `);
}
```
{: codeblock}

#### Get all features
{: #ac-js-get-all-features}

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

#### Evaluate a feature
{: #ac-js-feature-evaluation}

You can use the `feature.getCurrentValue(entityId, entityAttributes)` method to evaluate the value of the feature flag. This method returns one of the Enabled/Disabled/Overridden value based on the evaluation. The data type of returned value matches that of feature flag. Pass a unique `entityId` as the parameter to perform the feature flag evaluation.

```javascript
const entityId = 'john_doe';
const entityAttributes = {
   city: 'Bangalore',
   country: 'India',
};

const featureValue = feature.getCurrentValue(entityId, entityAttributes);
```
{: codeblock}

Where:
- `entityId`: Id of the Entity. This will be a string identifier related to the Entity against which the feature is evaluated. For any entity to interact with App Configuration, it must provide a unique entity ID.
- `entityAttributes`: A JSON object consisting of the attribute name and their values that defines the specified entity. This is an optional parameter if the feature flag is not configured with any targeting definition. If the targeting is configured, then entityAttributes should be provided for the rule evaluation. An attribute is a parameter that is used to define a segment. The SDK uses the attribute values to determine if the specified entity satisfies the targeting rules, and returns the appropriate feature flag value.

#### Get single property
{: #ac-js-get-single-property}

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
{: #ac-js-get-all-properties}

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
{: #ac-js-property-evaluation}

Use the `property.getCurrentValue(entityId, entityAttributes)` method to evaluate the value of the property. This method returns the default property value or its overridden value based on the evaluation. The data type of returned value matches that of property.

```javascript
const entityId = 'john_doe';
const entityAttributes = {
   city: 'Bangalore',
   country: 'India',
   };

const propertyValue = property.getCurrentValue(entityId, entityAttributes);
```
{: codeblock}

Where:
- `entityId`: Id of the Entity. This will be a string identifier related to the Entity against which the property is evaluated. For any entity to interact with App Configuration, it must provide a unique entity ID.
- `entityAttributes`: A JSON object consisting of the attribute name and their values that defines the specified entity. This is an optional parameter if the property is not configured with any targeting definition. If the targeting is configured, then entityAttributes should be provided for the rule evaluation. An attribute is a parameter that is used to define a segment. The SDK uses the attribute values to determine if the specified entity satisfies the targeting rules, and returns the appropriate property value.

## Supported data types
{: #ac-js-supported-data-types}

You can configure feature flags and properties with {{site.data.keyword.appconfig_short}}, supporting the following data types: Boolean, Numeric, and String. The String data type can be in the format of a text string, JSON, or YAML. The SDK processes each format as shown in the table.

| **Feature or Property value** | **Data type** | **Data format** | **Type of data returned by `getCurrentValue()`** | **Example output** |
| -- | -- | -- | -- | -- |
| `true` | BOOLEAN | not applicable | `boolean` | `true` |
| `25` | NUMERIC | not applicable | `number` | `25` |
| "a string text" | STRING | TEXT | `string` | `a string text` |
| `{"firefox": {`  \n `"name": "Firefox",`  \n  `"pref_url": "about:config"`  \n }} | STRING | JSON | `org.json.JSONObject` | `{"firefox":{"name":"Firefox","pref_url":"about:config"}}` |
|  `men:`  \n   `- John Smith`   \n`- Bill Jones`\n `women:`  \n   `- Mary Smith`   \n`- Susan Williams` | STRING | YAML | `java.lang.String` | `"men:\n  - John Smith\n  - Bill Jones\women:\n  - Mary Smith\n  - Susan Williams"`  |
{: caption="Table 1. Example outputs" caption-side="bottom"}

### Feature flag usage example
{: #ac-js-feature-flag}

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

### Property usage example
{: #ac-js-property}

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

### Listen to the feature or property changes
{: #ac-js-feature-prop-change}

To listen to the data changes, add the following code in your application:

```javascript
client.emitter.on('configurationUpdate', () => {
    // add your code
})
```
{: codeblock}
