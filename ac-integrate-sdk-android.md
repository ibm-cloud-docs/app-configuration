---

copyright:
  years: 2021, 2023
lastupdated: "2023-05-26"

keywords: app-configuration, app configuration, integrate sdk, android sdk, android, kotlin, java

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# App Configuration client SDK for Android
{: #ac-integrate-sdks-android}

{{site.data.keyword.appconfig_short}} service provides Android client SDK to integrate with your Android application that is written in Kotlin or Java programming language.
{: shortdesc}

## Prerequisites
{: #ac-integrate-ff-sdk-android-prereqs}

Following are the prerequisites for using the {{site.data.keyword.appconfig_short}} service SDK for Android:

- Android API level 22 or later
- [Android Studio](https://developer.android.com/studio/index.html){: external}
- [Gradle](https://gradle.org/install){: external}

## Integrating client SDK for Android app written in Kotlin
{: #ac-integrate-ff-sdk-android-kotlin}

{{site.data.keyword.appconfig_short}} service provides Android client SDK to integrate with your Android application. You can evaluate the values of your property and feature flag by integrating the SDK.

1. Install the SDK by using either one of the options:
   - [Download](https://github.com/IBM/appconfiguration-android-client-sdk) and import the package to your Android studio project.
   - Get the package through Gradle by adding the:
      - Add {{site.data.keyword.appconfig_short}} Android client SDK dependency to Project level `build.gradle` file.

         ```javascript
         repositories {
             mavenCentral()
         }
         ```
         {: codeblock}

      - Add {{site.data.keyword.appconfig_short}} Android client SDK dependency to Module level `build.gradle` file.

         ```javascript
         dependencies {
            implementation "com.ibm.cloud:appconfiguration-android-sdk:0.3.1"
         }
         ```
         {: codeblock}

1. Configure the `AndroidManifest.xml` file for internet permission.

   ```xml
   <uses-permission android:name="android.permission.INTERNET"/>
   ```
   {: codeblock}

1. Initialize the SDK.

   ```kotlin
   val appConfiguration = AppConfiguration.getInstance()

   appConfiguration.init( application,
                        "region",
                        "guid",
                        "apikey")

   //To start the configuration fetching operation, set the collectionId and environmentId in the following way.
    appConfiguration.setContext("collectionId","environmentId")
   ```
   {: codeblock}

   Where:
   - `region` - Region name where the service instance is created. Use `AppConfiguration.REGION_US_SOUTH` for Dallas, `AppConfiguration.REGION_US_EAST` for Washington DC, `AppConfiguration.REGION_EU_GB` for London, and `AppConfiguration.REGION_AU_SYD` for Sydney.
   - `guid` - GUID of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the dashboard.
   - `apikey` - ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the dashboard.
   - `collectionId` - ID of the collection created in {{site.data.keyword.appconfig_short}} service instance under the Collections section.
   - `environmentId` -  Id of the environment created in App Configuration service instance under the Environments section.

1. Set listener for feature or property data changes

   ```kotlin
   appConfiguration.registerConfigurationUpdateListener(object : ConfigurationUpdateListener {

       override fun onConfigurationUpdate() {
           // ADD YOUR CODE
       }
   })
   ```
   {: codeblock}

### Examples for using property and feature-related APIs for Android app that is written in Kotlin
{: #ac-integrate-ff-example-android-kotlin}

- **Get single feature**

   ```kotlin
   val feature: Feature? = appConfiguration.getFeature("featureId")
   ```
   {: codeblock}

- **Get all features**

   ```kotlin
   val features: HashMap<String, Feature>? = appConfiguration.getFeatures();
   ```
   {: codeblock}

- **Feature evaluation**

   You can use the `feature.getCurrentValue()` method to evaluate the value of the feature flag. Pass a unique `entityId` as the parameter to perform the feature flag evaluation. If the feature flag is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a *JSONObject*.

   ```kotlin
   JSONObject entityAttributes = new JSONObject();
   try {
       entityAttributes.put("city", "Bangalore");
       entityAttributes.put("country", "India");
   } catch (JSONException e) {
       e.printStackTrace();
   }

   val appConfiguration = AppConfiguration.getInstance()
   val feature: Feature? = appConfiguration.getFeature("featureId")

   if (feature?.getFeatureDataType() === Feature.FeatureType.NUMERIC) {
       val value = feature.getCurrentValue("entityId", entityAttributes)
   } else if (feature?.getFeatureDataType() === Feature.FeatureType.BOOLEAN) {
       val value = feature.getCurrentValue("entityId", entityAttributes)
   } else if (feature?.getFeatureDataType() === Feature.FeatureType.STRING) {
       val value = feature.getCurrentValue("entityId", entityAttributes)
   }
   ```
   {: codeblock}

- **Get single property**

   ```kotlin
   val property: Property? = appConfiguration.getProperty("propertyId")
   ```
   {: codeblock}

- **Get all properties**

   ```kotlin
   val properties: HashMap<String, Property>? = appConfiguration.getProperties();
   ```
   {: codeblock}

- **Property evaluation**

   You can use the `property.getCurrentValue()` method to evaluate the value of the property. Pass a unique `entityId` as the parameter to perform the property evaluation. If the property is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a *JSONObject*.

   ```kotlin
   JSONObject entityAttributes = new JSONObject();
   try {
       entityAttributes.put("city", "Bangalore");
       entityAttributes.put("country", "India");
   } catch (JSONException e) {
       e.printStackTrace();
   }

   val appConfiguration = AppConfiguration.getInstance()
   val property: Property? = appConfiguration.getProperty("propertyId")
   val value = property.getCurrentValue("entityId", entityAttributes)
   ```
   {: codeblock}

### Supported data types
{: #ac-integrate-data-types-kotlin}

App Configuration service configures the feature flag and properties in the following data types: Boolean, Numeric, String. The String data type can be of the format of a text string, JSON or YAML. Accordingly, the SDK processes each format as shown in Table 1.

| **Feature or Property value** | **Data type** | **Data format** | **Type of data returned by `getCurrentValue()`** | **Example output** |
| -- | -- | -- | -- | -- |
| `true` | BOOLEAN | not applicable | `java.lang.Boolean` | `true` |
| `25` | NUMERIC | not applicable | `java.lang.Integer` | `25` |
| "a string text" | STRING | TEXT | `java.lang.String` | `a string text` |
| `{"firefox": {`  \n `"name": "Firefox",`  \n  `"pref_url": "about:config"`  \n }} | STRING | JSON | `org.json.JSONObject` | `{"firefox":{"name":"Firefox","pref_url":"about:config"}}` |
|  `men:`  \n   `- John Smith`   \n`- Bill Jones`\n `women:`  \n   `- Mary Smith`   \n`- Susan Williams` | STRING | YAML | `java.lang.String` | `"men:\n  - John Smith\n  - Bill Jones\women:\n  - Mary Smith\n  - Susan Williams"`  |
{: caption="Table 1. Example outputs" caption-side="bottom"}

#### Feature flag
{: #ac-feat-flag}

```kotlin
val feature: Feature? = appConfiguration.getFeature("json-feature")
feature.getFeatureDataType(); // STRING
feature.getFeatureDataFormat(); // JSON

// Example below (traversing the returned JSONObject)
if (feature != null) {
   val result = feature.getCurrentValue(entityId, entityAttributes) as JSONObject
   result.get("key") // returns the value of the key
}

val feature: Feature? = appConfiguration.getFeature("yaml-feature")
feature.getFeatureDataType(); // STRING
feature.getFeatureDataFormat(); // YAML
feature.getCurrentValue(entityId, entityAttributes); // returns the stringified yaml (check Table 1)
```
{: codeblock}

#### Property
{: #ac-property}

```javascript
val property: Property? = appConfiguration.getProperty("json-property")
property.getPropertyDataType(); // STRING
property.getPropertyDataFormat(); // JSON

// Example below (traversing the returned JSONObject)
if (property != null) {
  val result = property.getCurrentValue(entityId, entityAttributes) as JSONObject
  result.get("key") // returns the value of the key
}

val property: Property? = appConfiguration.getProperty("yaml-property")
property.getPropertyDataType(); // STRING
property.getPropertyDataFormat(); // YAML
property.getCurrentValue(entityId, entityAttributes); // returns the stringified yaml (check above Table 1)
```
{: codeblock}

- Force fetch the configurations from server.

   ```kotlin
   appConfiguration.fetchConfigurations()
   ```
   {: codeblock}

## Integrating client SDK for Android app written in Java
{: #ac-integrate-ff-sdk-android-java}

{{site.data.keyword.appconfig_short}} service provides Android client SDK to integrate with your Android application. You can evaluate the values of your property and feature flag by integrating the SDK.

1. Install the SDK by using either one of the options:
   - [Download](https://github.com/IBM/appconfiguration-android-client-sdk) and import the package to your Android studio project.
   - Get the package through Gradle by adding:
      - Add {{site.data.keyword.appconfig_short}} Android client SDK dependency to Project level `build.gradle` file.

         ```javascript
         repositories {
            mavenCentral()
         }
         ```
         {: codeblock}

      - Add {{site.data.keyword.appconfig_short}} Android client SDK dependency to Module level `build.gradle` file.

         ```javascript
         dependencies {
            implementation "com.ibm.cloud:appconfiguration-android-sdk:0.3.1"
         }
         ```
         {: codeblock}

1. Configure the `AndroidManifest.xml` file for internet permission.

   ```xml
   <uses-permission android:name="android.permission.INTERNET"/>
   ```
   {: codeblock}

1. Integrate Kotlin to your Java project with these steps:

   - Add the Kotlin Gradle plug-in to the Module level `build.gradle`

      ```javascript
      dependencies {
        classpath "com.android.tools.build:gradle:4.1.1"
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
      }
      ```
      {: codeblock}

   - Add `kotlin-android` plugin to the App level `build.gradle`

      ```javascript
      plugins {
         id 'com.android.application'
         id 'kotlin-android'
      }
      ```
      {: codeblock}

1. Initialize the SDK.

   ```java
   AppConfiguration appConfiguration = AppConfiguration.getInstance();
   appConfiguration.init(getApplication(), "region", "guid", "apikey");

   // To start the configuration fetching operation, set the collectionId in the following way.
   appConfiguration.setContext("collectionId", "environmentId");
   ```
   {: codeblock}

   Where:
   - `region` - Region name where the service instance is created. Use `AppConfiguration.REGION_US_SOUTH` for Dallas, `AppConfiguration.REGION_US_EAST` for Washington DC, `AppConfiguration.REGION_EU_GB` for London, and `AppConfiguration.REGION_AU_SYD` for Sydney.
   - `guid` - GUID of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the dashboard.
   - `apikey` - ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the dashboard.
   - `collectionId` - ID of the collection created in {{site.data.keyword.appconfig_short}} service instance.
   - `environmentId`- ID of the environment created in App Configuration service instance under the Environments section.

1. Listen to the feature changes

   ```java
   appConfiguration.registerConfigurationUpdateListener(new ConfigurationUpdateListener() {
       @Override
       public void onConfigurationUpdate() {
          // ADD YOUR CODE
       }
   });
   ```
   {: codeblock}

### Examples for using property and feature-related APIs for Android apps written in Java
{: #ac-integrate-ff-example-android-java}

Refer to the examples for using the property and feature-related APIs.

- **Get single feature**

   ```java
   Feature feature = appConfiguration.getFeature("featureId");
   ```
   {: codeblock}

- **Get all features**

   ```java
   HashMap<String,Feature> features =  appConfiguration.getFeatures();
   ```
   {: codeblock}

- **Feature evaluation**

   You can use the `feature.getCurrentValue()` method to evaluate the value of the feature flag. Pass a unique `entityId` as the parameter to perform the feature flag evaluation. If the feature flag is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a *JSONObject*.

   ```java
   JSONObject entityAttributes = new JSONObject();

   try {
       entityAttributes.put("city", "Bengaluru");
       entityAttributes.put("country", "India");
   } catch (JSONException e) {
       e.printStackTrace();
   }

   AppConfiguration appConfiguration = AppConfiguration.getInstance();
   Feature feature = appConfiguration.getFeature("featureId")
   if(feature != null)
       switch (feature.getFeatureDataType())
           case STRING:
               String value = (String) feature.getCurrentValue(entityId, entityAttributes);
               System.out.println(value);
               break;
           case BOOLEAN:
               Boolean boolVal = (Boolean) feature.getCurrentValue(entityId, entityAttributes);
               System.out.println(boolVal);
               break;
           case NUMERIC:
               Integer intVal = (Integer) feature.getCurrentValue(entityId, entityAttributes);
               System.out.println(intVal);
               break;
       }
   }
   ```
   {: codeblock}

- **Get single property**

   ```java
   Property property = appConfiguration.getProperty("propertyId");
   ```
   {: codeblock}

- **Get all properties**

   ```java
   HashMap<String,Property> properties =  appConfiguration.getProperties();
   ```
   {: codeblock}

- **Property evaluation**

   You can use the `property.getCurrentValue()` method to evaluate the value of the property. Pass a unique `entityId` as the parameter to perform the property evaluation. If the property is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a *JSONObject*.

   ```java
   JSONObject entityAttributes = new JSONObject();

   try {
       entityAttributes.put("city", "Bengaluru");
       entityAttributes.put("country", "India");
   } catch (JSONException e) {
       e.printStackTrace();
   }

   AppConfiguration appConfiguration = AppConfiguration.getInstance();
   Property property = appConfiguration.getProperty("propertyId");
   String value = (String) property.getCurrentValue(entityId, entityAttributes);
   ```
   {: codeblock}

### Supported data types
{: #ac-integrate-data-types-java}

App Configuration service configures the feature flag and properties in the following data types: Boolean, Numeric, String. The String data type can be of the format of a text string, JSON, or YAML. The SDK processes each format accordingly as shown in Table 1.

#### Feature Flag
{: #ac-feat-flag1}

```java
Feature feature = appConfiguration.getFeature("json-feature");
feature.getFeatureDataType(); // STRING
feature.getFeatureDataFormat(); // JSON

// Example below (traversing the returned JSONObject)
if (feature != null) {
  JSONObject result = (JSONObject) feature.getCurrentValue(entityId, entityAttributes);
  result.get("key") // returns the value of the key
}

Feature feature = appConfiguration.getFeature("yaml-feature");
feature.getFeatureDataType(); // STRING
feature.getFeatureDataFormat(); // YAML
feature.getCurrentValue(entityId, entityAttributes); // returns the stringified yaml (check above Table 1)
```
{: codeblock}

#### Property
{: #ac-prop1}

```java
Property property = appConfiguration.getProperty("json-property");
property.getPropertyDataType(); // STRING
property.getPropertyDataFormat(); // JSON

// Example below (traversing the returned JSONObject)
if (property != null) {
  JSONObject result = (JSONObject) property.getCurrentValue(entityId, entityAttributes);
  result.get("key") // returns the value of the key
}

Property property = appConfiguration.getProperty("yaml-property");
property.getPropertyDataType(); // STRING
property.getPropertyDataFormat(); // YAML
property.getCurrentValue(entityId, entityAttributes); // returns the stringified yaml (check Table 1)
```
{: codeblock}

- Force fetch the configurations from server.

   ```java
   appConfiguration.fetchConfigurations()
   ```
   {: codeblock}
