---

copyright:
  years: 2021
lastupdated: "2021-07-19"

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

1. Install the SDK using one of the following ways.

   Using **Maven**:

      ```xml
      <dependency>
         <groupId>com.ibm.cloud</groupId>
         <artifactId>appconfiguration-java-sdk</artifactId>
         <version>0.1.0</version>
      </dependency>
      ```
      {: codeblock}

   Get the package through **Gradle** by adding the following:

      ```sh
      implementation group: 'com.ibm.cloud', name: 'appconfiguration-java-sdk', version: '0.1.0'
      ```
      {: codeblock}

1. In your Java microservice or application, include the SDK with:

   ```java
   import com.ibm.cloud.appconfiguration.sdk.AppConfiguration
   ```
   {: codeblock}

1. Initialize the SDK to connect with your {{site.data.keyword.appconfig_short}} service instance.
   {: #ac-init-java-sdk}

      ```java
      AppConfiguration appConfiguration = AppConfiguration.getInstance();

      String guid =  "guid"
      String apikey = "apikey";

      appConfiguration.init(AppConfiguration.REGION_US_SOUTH, guid, apikey);

      String collectionId = "collectionId";
      String environmentId = "environmentId";
      // Set the collectionId and environmentId to start the configuration fetching operation.
      appConfiguration.setContext(collectionId, environmentId)
      ```
      {: codeblock}

      where,
      - region: Region name where the service instance is created. Use `AppConfiguration.REGION_US_SOUTH` for Dallas, `AppConfiguration.REGION_EU_GB` for London, and `AppConfiguration.REGION_AU_SYD` for Sydney.
      - guid: GUID of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
      - apiKey: ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
      - collectionId: Id of the collection created in {{site.data.keyword.appconfig_short}} service instance under the Collections section.
      - environmentId : Id of the environment created in App Configuration service instance under the Environments section.

1. *Optional*: You can work [offline](/docs/app-configuration?topic=app-configuration-ac-offline) with local configuration file and perform [feature and property related operations](#ac-java-example). After setting the `appConfiguration.init(AppConfiguration.REGION_US_SOUTH, guid, apikey)`, follow the below step:

   ```java
   String configurationFile = "custom/userJson.json";
   Boolean liveConfigUpdateEnabled = true;

   // Set the collectionId and environmentId to start the configuration fetching operation.
  appConfiguration.setContext(collectionId, environmentId, configurationFile, liveConfigUpdateEnabled);
   ```
   {: codeblock}

   where,
   - configurationFile: Path to the JSON file which contains configuration details.
   - liveConfigUpdateEnabled: Set this value to `false` if the new configuration values shouldn't be fetched from the server. Make sure to provide a proper JSON file in the `configurationFile` path. By default, this value is enabled.

### Examples for using feature and property related APIs
{: #ac-java-example}

Refer to the below examples for using the feature and property related APIs.

#### Get single feature
{: #ac-java-get-single-feature}

```java
Feature feature = appConfiguration.getFeature("feature_id");

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
HashMap<String, Feature> features = appConfiguration.getFeatures();
```
{: codeblock}

#### Feature evaluation
{: #ac-java-feature-evaluation}

You can use the `feature.getCurrentValue(entityId, entityAttributes)` method to evaluate the value of the feature flag. You should pass an unique `entityId` as the parameter to perform the feature flag evaluation. If the feature flag is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a JSONObject.

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
Property property = appConfiguration.getProperty("property_id");

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
HashMap<String, Property> property = appConfiguration.getProperties();
```
{: codeblock}

#### Property evaluation
{: #ac-java-property-evaluation}

You can use the `property.getCurrentValue(entityId, entityAttributes)` method to evaluate the value of the property.

You should pass an unique `entityId` as the parameter to perform the property evaluation. If the property is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a JSONObject.

```java
JSONObject entityAttributes = new JSONObject();
entityAttributes.put("city", "Bangalore");
entityAttributes.put("country", "India");

String value = (String) property.getCurrentValue("entityId", entityAttributes);
```
{: codeblock}

#### Set listener for feature or property changes
{: #ac-java-listen-feature-changes}

To listen to the data changes, add the following code in your application:

```java
appConfiguration.registerConfigurationUpdateListener(new ConfigurationUpdateListener() {
    @Override
    public void onConfigurationUpdate() {
       System.out.println("Got feature/property now");
    }
});
```
{: codeblock}

#### Fetch latest data
{: #ac-java-fetch-latest-data}

```java
appConfiguration.fetchConfigurations()
```
{: codeblock}
