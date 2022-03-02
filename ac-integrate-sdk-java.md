---

copyright:
  years: 2022
lastupdated: "2022-03-01"

keywords: app-configuration, app configuration, integrate sdk, java sdk, java server sdk, java

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
{:go: .ph data-hd-programlang='go'}

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
         <version>0.2.3</version>
      </dependency>
      ```
      {: codeblock}

   Get the package through **Gradle** by adding:

      ```sh
      implementation group: 'com.ibm.cloud', name: 'appconfiguration-java-sdk', version: '0.2.3'
      ```
      {: codeblock}

2. In your Java microservice or application, include the SDK with:

   ```java
   import com.ibm.cloud.appconfiguration.sdk.AppConfiguration
   ```
   {: codeblock}

3. Initialize the SDK to connect with your {{site.data.keyword.appconfig_short}} service instance.
   {: #ac-init-java-sdk}

     ```java
      AppConfiguration appConfigClient = AppConfiguration.getInstance();

      String guid =  "guid"
      String apikey = "apikey";

      appConfigClient.init(AppConfiguration.REGION_US_SOUTH, guid, apikey);

      String collectionId = "collectionId";
      String environmentId = "environmentId";
      // Set the collectionId and environmentId to start the configuration fetching operation.
      appConfigClient.setContext(collectionId, environmentId)
      ```
      {: codeblock}

      Where,
      - region: Region name where the service instance is created. Use `AppConfiguration.REGION_US_SOUTH` for Dallas, `AppConfiguration.REGION_EU_GB` for London, `AppConfiguration.REGION_AU_SYD` for Sydney and `AppConfiguration.REGION_US_EAST` for Washington DC. 
      - guid: GUID of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
      - apiKey: ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
      - collectionId: ID of the collection created in {{site.data.keyword.appconfig_short}} service instance under the Collections section.
      - environmentId: ID of the environment created in App Configuration service instance under the Environments section.
      

The **`init()`** and **`setContext()`** are the initialisation methods and should be invoked **only once** using appConfigClient. The appConfigClient, once initialised, can be obtained across modules using **`AppConfiguration.getInstance()`**.  [See this example below](/docs/app-configuration?topic=app-configuration-ac-java#fetching-the-appconfig_client-across-other-modules).
   
{: important}

### Option to use a persistent cache for configuration

{: #ac-java-persistent-cache}

In order for your application and SDK to continue operations even during the unlikely scenario of an {{site.data.keyword.appconfig_short}} service downtime, across your application restarts, you can configure the SDK to work by using a persistent cache. The SDK uses the persistent cache to store the {{site.data.keyword.appconfig_short}} data that is available across your application restarts.

```java
// 1. default (without persistent cache)
    appConfigClient.setContext(collectionId, environmentId);

// 2. optional (with persistent cache)
    ConfigurationOptions configOptions = new ConfigurationOptions();
    configOptions.setPersistentCacheDirectory("/var/lib/docker/volumes/");
    appConfigClient.setContext(collectionId, environmentId, configOptions);

```

{: codeblock}

where,
- persistentCacheDirectory: Absolute path to a directory which has read and write permission for the user. The SDK will create a file - `appconfiguration.json` in the specified directory, and it will be used as the persistent cache to store the {{site.data.keyword.appconfig_short}} service information.
  
   
When persistent cache is enabled, the SDK will keep the last known good configuration at the persistent cache. In the case of the {{site.data.keyword.appconfig_short}} server being unreachable, the latest configurations at the persistent cache is loaded to the application to continue working.

### Offline options
{: #ac-java-offline}

The SDK is also designed to serve configurations, and perform feature flag and property evaluations without being connected to {{site.data.keyword.appconfig_short}} service.

```java
ConfigurationOptions configOptions = new ConfigurationOptions();
configOptions.setBootstrapFile("saflights/flights.json");
configOptions.setLiveConfigUpdateEnabled(false);
```

{: codeblock}

where,

- bootstrapFile: Absolute path of the JSON file, which contains configuration details. Make sure to provide a proper JSON file. You can generate this file by using `ibmcloud ac config` command of the IBM Cloud App Configuration CLI.

- liveConfigUpdateEnabled: Live configuration update from the server. Set this value to `False` if the new configuration values must not be fetched from the server. By default, this value is set to True.


### Examples for using feature and property related APIs
{: #ac-use-java-example}

Refer to the below examples for using the feature and property related APIs.

#### Get single feature
{: #ac-java-get-single-feature}

```java
  Feature feature = appConfigClient.getFeature("feature_id");

if (feature) {
    System.out.println("Feature Name : " + feature.getFeatureName());
    System.out.println("Feature Id : " + feature.getFeatureId());
    System.out.println("Feature Type : " + feature.getFeatureDataType());
    System.out.println("Feature is enabled : " + feature.isEnabled());
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
JSONObject entityAttributes = new JSONObject();
entityAttributes.put("city", "Bangalore");
entityAttributes.put("country", "India");

String value = (String) feature.getCurrentValue("entityId", entityAttributes);
```
{: codeblock}

#### Get single property
{: #ac-java-get-single-property}

```java
Property property = appConfigClient.getProperty("property_id");

if (property) {
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

You can use the `property.getCurrentValue(entityId, entityAttributes)` method to evaluate the value of the property.

You must pass a unique `entityId` as the parameter for the property evaluation. If the property is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a JSONObject.

```java
JSONObject entityAttributes = new JSONObject();
entityAttributes.put("city", "Bangalore");
entityAttributes.put("country", "India");

String value = (String) property.getCurrentValue("entityId", entityAttributes);
```
{: codeblock}

## Supported data types
{: #ac-integrate-data-types}

App Configuration service allows you to configure feature flags and properties with the following data types: Boolean,
Numeric, String. The String data type can be of the format of a TEXT string, JSON, or YAML. The SDK processes each
format as shown in the below table.

| **Feature or Property value**                                                                                      | **Data type** | **Data format** | **Type of data returned <br> by `GetCurrentValue()`** | **Example output**                                                   |
| ------------------------------------------------------------------------------------------------------------------ | ------------ | -------------- | ----------------------------------------------------- | -------------------------------------------------------------------- |
| `true`                                                                                                             | BOOLEAN      | not applicable | `java.lang.Boolean`                                                | `true`                                                               |
| `25`                                                                                                               | NUMERIC      | not applicable | `java.lang.Integer`                                             | `25`                                                                 |
| "a string text"                                                                                                    | STRING       | TEXT           | `java.lang.String`                                              | `a string text`                                                      |
| <pre>{<br>  "firefox": {<br>    "name": "Firefox",<br>    "pref_url": "about:config"<br>  }<br>}</pre> | STRING       | JSON           | `org.json.JSONObject`                              | `{"firefox": {"name": "Firefox", "pref_url": "about:config"}}` |
| <pre>men:<br>  - John Smith<br>  - Bill Jones<br>women:<br>  - Mary Smith<br>  - Susan Williams</pre>  | STRING       | YAML           | `java.lang.String`                              | <pre>"men:\n - John Smith\n - Bill Jones\nwomen:\n - Mary Smith\n - Susan Williams"</pre> |
{: caption="Table 1. Example outputs" caption-side="top"}

#### Feature flag
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
    property.getPropertyDataType()     // STRING
    property.getPropertyDataFormat()   // JSON
    property.getCurrentValue(entityId, entityAttributes) // JSONObject or JSONArray is returned

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
    property.getPropertyDataType()     // STRING
    property.getPropertyDataFormat()   // YAML
    property.getCurrentValue(entityId, entityAttributes) // Yaml String is returned

}
```
{: codeblock}


#### Set listener for feature or property changes
{: #ac-java-listen-feature-and-property-changes}

The SDK provides mechanism to notify you in real-time when feature flag's or property's configuration changes. You can subscribe to configuration changes using the same appconfig_client.

```java
appConfigClient.registerConfigurationUpdateListener(new ConfigurationUpdateListener() {
    @Override
    public void onConfigurationUpdate() {
       System.out.println("Got feature/property now");
    }
});
```
{: codeblock}

#### Fetch most recent data
{: #ac-java-fetch-latest-data}

```java
appConfigClient.fetchConfigurations()
```
{: codeblock}
