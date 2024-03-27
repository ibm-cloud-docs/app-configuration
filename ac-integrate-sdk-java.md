---

copyright:
  years: 2022, 2024
lastupdated: "2024-03-25"

keywords: app-configuration, app configuration, integrate sdk, java sdk, java server sdk, java

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# App Configuration server SDK for Java
{: #ac-java}

{{site.data.keyword.appconfig_short}} service provides SDKs to integrate with your applications, microservices, and distributed environments.
{: shortdesc}

## Integrating server SDK for Java
{: #ac-integrate-java-sdk}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Java applications. You can evaluate the values of your feature flag by integrating the {{site.data.keyword.appconfig_short}} SDK.

1. Install the SDK in one of the following ways.

   Using **Maven**

      ```xml
      <dependency>
         <groupId>com.ibm.cloud</groupId>
         <artifactId>appconfiguration-java-sdk</artifactId>
         <version>0.3.3</version>
      </dependency>
      ```
      {: codeblock}

   Get the package through **Gradle** by adding:

      ```sh
      implementation group: 'com.ibm.cloud', name: 'appconfiguration-java-sdk', version: '0.3.3'
      ```
      {: codeblock}

1. In your Java microservice or application, include the SDK with:

   ```java
   import com.ibm.cloud.appconfiguration.sdk.AppConfiguration;
   ```
   {: codeblock}

1. Initialize the SDK to connect with your {{site.data.keyword.appconfig_short}} service instance.
   {: #ac-init-java-sdk}

   ```java
   String region = AppConfiguration.REGION_US_SOUTH;
   String guid = "guid";
   String apikey = "apikey";

   String collectionId = "airlines-webapp";
   String environmentId = "dev";

   AppConfiguration appConfigClient = AppConfiguration.getInstance();
   appConfigClient.init(region, guid, apikey);
   appConfigClient.setContext(collectionId, environmentId);
   ```
   {: codeblock}

   Where,
   - `region`: Region name where the service instance is created. Use `AppConfiguration.REGION_US_SOUTH` for Dallas, `AppConfiguration.REGION_US_EAST` for Washington DC, `AppConfiguration.REGION_EU_GB` for London, `AppConfiguration.REGION_EU_DE` for Frankfurt and `AppConfiguration.REGION_AU_SYD` for Sydney.
   - `guid`: GUID of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - `apiKey`: ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - `collectionId`: ID of the collection created in {{site.data.keyword.appconfig_short}} service instance under the Collections section.
   - `environmentId`: ID of the environment created in App Configuration service instance under the Environments section.

The **`init()`** and **`setContext()`** are the initialization classes and must be invoked **only once** by using `appConfigClient`. The appConfigClient, when initialized, can be obtained across classes by using **`AppConfiguration.getInstance()`**. For more information, see [Fetching the appConfigClient across other classes](#fetching-the-appConfigClient-across-other-classes).
{: important}

### Using private endpoints
{: #ac-java-private-endpoints}

Set the SDK to connect to {{site.data.keyword.appconfig_short}} service by using a private endpoint that is accessible only through the {{site.data.keyword.cloud_notm}} private network.

```java
appConfigClient.usePrivateEndpoint(true);
```
{: codeblock}

This must be done before calling the `init` function on the SDK.
{: note}

### Option to use a persistent cache for configuration
{: #ac-java-persistent-cache}

For your application and SDK to continue operations during the unlikely scenario of an {{site.data.keyword.appconfig_short}} service downtime, across your application restarts, you can configure the SDK to work by using a persistent cache. The SDK uses the persistent cache to store the {{site.data.keyword.appconfig_short}} data that is available across your application restarts.

```java
// 1. default (without persistent cache)
    appConfigClient.setContext(collectionId, environmentId);

// 2. optional (with persistent cache)
    ConfigurationOptions configOptions = new ConfigurationOptions();
    configOptions.setPersistentCacheDirectory("/var/lib/docker/volumes/");
    appConfigClient.setContext(collectionId, environmentId, configOptions);
```
{: codeblock}

Where:
- `persistentCacheDirectory`: Absolute path to a directory that has read and write permission for the user. The SDK creates a file - `appconfiguration.json` in the specified directory, and it is used as the persistent cache to store the {{site.data.keyword.appconfig_short}} service information.

When persistent cache is enabled, the SDK keeps the last known good configuration at the persistent cache. If the {{site.data.keyword.appconfig_short}} server being unreachable, the latest configurations at the persistent cache are loaded to the application to continue working.

Ensure that the cache file is not lost or deleted in any case. For example, consider the case when a kubernetes pod is restarted and the cache file (`appconfiguration.json`) was stored in ephemeral volume of the pod. As pod gets restarted, kubernetes destroys the ephermal volume in the pod, as a result the cache file gets deleted. So, make sure that the cache file created by the SDK is always stored in persistent volume by providing the correct absolute path of the persistent directory.
{: important}

### Offline options
{: #ac-java-offline}

The SDK is also designed to serve configurations, and perform feature flag and property evaluations without being connected to {{site.data.keyword.appconfig_short}} service.

```java
ConfigurationOptions configOptions = new ConfigurationOptions();
configOptions.setBootstrapFile("saflights/flights.json");
configOptions.setLiveConfigUpdateEnabled(false);
appConfigClient.setContext(collectionId, environmentId, configOptions);
```
{: codeblock}

Where:
- `bootstrapFile`: Absolute path of the JSON file, which contains configuration details. Make sure to provide a proper JSON file. You can generate this file by using `ibmcloud ac export` command of the {{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_short}} CLI.
- `liveConfigUpdateEnabled`: Live configuration update from the server. Set this value to `false` if the new configuration values must not be fetched from the server. By default, this value is set to `true`.

### Examples for using feature and property related APIs
{: #ac-use-java-example}

See the following examples for using the feature and property related APIs.

#### Get single feature
{: #ac-java-get-single-feature}

```java
Feature feature = appConfigClient.getFeature("online-check-in");

if (feature != null) {
    System.out.println("Feature Name : " + feature.getFeatureName());
    System.out.println("Feature Id : " + feature.getFeatureId());
    System.out.println("Feature Type : " + feature.getFeatureDataType());
    System.out.println("Is feature enabled? : " + feature.isEnabled());
}
```
{: codeblock}

#### Get all features
{: #ac-java-get-all-features}

```java
HashMap<String, Feature> features = appConfigClient.getFeatures();
```
{: codeblock}

#### Feature evaluation
{: #ac-java-feature-evaluation}

You can use the `feature.getCurrentValue(entityId, entityAttributes)` method to evaluate the value of the feature flag. You must pass a unique `entityId` as the parameter for the feature flag evaluation. If the feature flag is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a JSONObject.

```java
String entityId = "john_doe";
JSONObject entityAttributes = new JSONObject();
entityAttributes.put("city", "Bangalore");
entityAttributes.put("country", "India");

String value = (String) feature.getCurrentValue(entityId, entityAttributes);
```
{: codeblock}

- `entityId`: Id of the entity. This is a string identifier related to the entity against which the feature is evaluated. For example, an entity might be an instance of an app that runs on a mobile device, a microservice that runs on the cloud, or a component of infrastructure that runs that microservice. For any entity to interact with {{site.data.keyword.appconfig_short}}, it must provide a unique entity ID.

- `entityAttributes`: A JSON object consisting of the attribute name and their values that define the specified entity. This is an optional parameter if the feature flag is not configured with any targeting definition. If the targeting is configured, then `entityAttributes` should be provided for the rule evaluation. An attribute is a parameter that is used to define a segment. The SDK uses the attribute values to determine whether the specified entity satisfies the targeting rules, and returns the appropriate feature flag value.

#### Get single property
{: #ac-java-get-single-property}

```java
Property property = appConfigClient.getProperty("check-in-charges");

if (property != null) {
    System.out.println("Property Name : " + property.getPropertyName());
    System.out.println("Property Id : " + property.getPropertyId());
    System.out.println("Property Type : " + property.getPropertyDataType());
}
```
{: codeblock}

#### Get all properties
{: #ac-java-get-all-property}

```java
HashMap<String, Property> property = appConfigClient.getProperties();
```
{: codeblock}

#### Property evaluation
{: #ac-java-property-evaluation}

You can use the `property.getCurrentValue(entityId, entityAttributes)` method to evaluate the value of the property. This method returns the default property value or its overridden value based on the evaluation.

```java
String entityId = "john_doe";
JSONObject entityAttributes = new JSONObject();
entityAttributes.put("city", "Bangalore");
entityAttributes.put("country", "India");

String value = (String) property.getCurrentValue(entityId, entityAttributes);
```
{: codeblock}

- `entityId`: Id of the entity. This is a string identifier related to the entity against which the property is evaluated. For example, an entity might be an instance of an app that runs on a mobile device, a microservice that runs on the cloud, or a component of infrastructure that runs that microservice. For any entity to interact with {{site.data.keyword.appconfig_short}}, it must provide a unique entity ID.

- `entityAttributes`: A JSON object consisting of the attribute name and their values that define the specified entity. This is an optional parameter if the property is not configured with any targeting definition. If the targeting is configured, then `entityAttributes` should be provided for the rule evaluation. An attribute is a parameter that is used to define a segment. The SDK uses the attribute values to determine whether the specified entity satisfies the targeting rules, and returns the appropriate property value.

### Fetching the `appConfigClient` across other classes
{: #fetching-the-appConfigClient-across-other-classes}

When the SDK is initialized, the `appConfigClient` can be obtained across other classes as shown:

```java
// **other classes**

import com.ibm.cloud.appconfiguration.sdk.AppConfiguration;
AppConfiguration appConfigClient = AppConfiguration.getInstance();

Feature feature = appConfigClient.getFeature("string-feature");
boolean enabled = feature.isEnabled();
String featureValue = (String) feature.getCurrentValue(entityId, entityAttributes);
```
{: codeblock}

## Supported data types
{: #ac-integrate-data-types}

App Configuration service allows you to configure feature flags and properties with the following data types: Boolean,
Numeric, String. The String data type can be of the format of a TEXT string, JSON, or YAML. The SDK processes each
format as shown in the table 1.

| **Feature or Property value** | **Data type** | **Data format** | **Type of data returned by `GetCurrentValue()`** | **Example output** |
| -- | -- | -- | -- | -- |
| `true` | BOOLEAN | not applicable | `bool` | `true` |
| `25` | NUMERIC | not applicable | `float64` | `25` |
| "a string text" | STRING | TEXT | `string` | `a string text` |
| `{"firefox": {`  \n `"name": "Firefox",`  \n  `"pref_url": "about:config"`  \n }} | STRING | JSON | `map[string]interface{}` | `map[browsers:map[firefox:map[name:Firefox pref_url:about:config]]]` |
|  `men:`  \n   `- John Smith`   \n`- Bill Jones`\n `women:`  \n   `- Mary Smith`   \n`- Susan Williams`  | STRING | YAML | `java.lang.String` | `"men:\n - John Smith\n - Bill Jones\women:\n - Mary Smith\n - Susan Williams"` |
{: caption="Table 1. Example outputs" caption-side="bottom"}

### Feature flag
{: #ac-java-example-ff}

```java
Feature feature = appConfigClient.getFeature("json-feature");
if (feature != null) {
   feature.getFeatureDataType();       // STRING
   feature.getFeatureDataFormat();     // JSON
   feature.getCurrentValue(entityId, entityAttributes); // JSONObject or JSONArray is returned
}

// Example Below
// input json :- [{"role": "developer", "description": "do coding"},{"role": "tester", "description": "do testing"}]
// expected output :- "do coding"

JSONArray tar_val = (JSONArray) feature.get_current_value(entityId, entityAttributes);
String expected_output = (String) ((JSONObject) tar_val.get(0)).get('description');

// input json :- {"role": "tester", "description": "do testing"}
// expected output :- "tester"

JSONObject tar_val = (JSONObject) feature.get_current_value(entityId, entityAttributes);
String expected_output = (String) tar_val.get('role');

Feature feature = appConfigClient.getFeature("yaml-feature");
if (feature != null) {
   feature.getFeatureDataType();       // STRING
   feature.getFeatureDataFormat();     // YAML
   feature.getCurrentValue(entityId, entityAttributes); // Yaml String is returned
}
```
{: codeblock}

#### Property
{: #ac-java-example-property}

```java
Property property = appConfigClient.getProperty("json-property");
if (property != null) {
   property.getPropertyDataType();     // STRING
   property.getPropertyDataFormat();   // JSON
   property.getCurrentValue(entityId, entityAttributes); // JSONObject or JSONArray is returned
}

// Example Below
// input json :- [{"role": "developer", "description": "do coding"},{"role": "tester", "description": "do testing"}]
// expected output :- "do coding"

JSONArray tar_val = (JSONArray) property.get_current_value(entityId, entityAttributes);
String expected_output = (String) ((JSONObject) tar_val.get(0)).get('description');

// input json :- {"role": "tester", "description": "do testing"}
// expected output :- "tester"

JSONObject tar_val = (JSONObject) property.get_current_value(entityId, entityAttributes);
String expected_output = (String) tar_val.get('role');

Property property = appConfigClient.getProperty("yaml-property");
if (property != null) {
   property.getPropertyDataType();     // STRING
   property.getPropertyDataFormat();   // YAML
   property.getCurrentValue(entityId, entityAttributes); // Yaml String is returned
}
```
{: codeblock}

#### Set listener for feature or property changes
{: #ac-java-listen-feature-and-property-changes}

The SDK provides mechanism to notify you in real time when feature flag's or property's configuration changes. You can subscribe to configuration changes by using the same appConfigClient.

```java
appConfigClient.registerConfigurationUpdateListener(new ConfigurationUpdateListener() {
   @Override
   public void onConfigurationUpdate() {
      System.out.println("Received updated configurations");
      // **add your code**
      // To find the effect of any configuration changes, you can call the feature or property related methods

      // Feature feature = appConfigClient.getFeature("numeric-feature");
      // Integer newValue = (Integer) feature.getCurrentValue(entityId, entityAttributes);
   }
});
```
{: codeblock}

#### Fetch most recent data
{: #ac-java-fetch-latest-data}

```java
appConfigClient.fetchConfigurations();
```
{: codeblock}
