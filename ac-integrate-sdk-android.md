---

copyright:
  years: 2021
lastupdated: "2021-01-13"

keywords: app-configuration, app configuration, integrate sdk, core sdk, android sdk, android, kotlin, java

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
{:kotlin: .ph data-hd-programlang='Kotlin'}

# App Configuration service SDK for Android
{: #ac-integrate-sdks-android}

{{site.data.keyword.appconfig_short}} service provides Android SDK to integrate with your Android application written in Kotlin or Java programming language. 
{:shortdesc}

## Prerequisites
{: #ac-integrate-ff-sdk-android-prereqs}

Following are the prerequisites for using the {{site.data.keyword.appconfig_short}} service SDK for Android:

- Android API level 17 or later
- [Android Studio](https://developer.android.com/studio/index.html){:external}
- [Gradle](https://gradle.org/install){:external}

## Integrating {{site.data.keyword.appconfig_short}} SDK
{: #ac-integrate-ff-sdk-android}

{{site.data.keyword.appconfig_short}} service provides Android SDK to integrate with your Android application. You can evaluate the values of your feature flag by integrating the SDK. 

1. Install the SDK using either one of the following option:
   - [Download]() and import the package to your Android studio project.
   - Get the package through Gradle by adding {{site.data.keyword.appconfig_short}} Android SDK dependency to Module level `build.gradle` file.

      ```javascript
      dependencies {
         implementation "com.ibm.appconfiguration.android:lib:1.0.0"
      }
      ```
      {:codeblock}

1. Configure the `AndroidManifest.xml` file for Internet permission.

   ```xml
   <uses-permission android:name="android.permission.INTERNET"/>
   ```
   {:codeblock}

1. *Optional*: Integrate Kotlin to your Java project with these steps:
   {:java}
   - Add the Kotlin gradle plugin to the Module level `build.gradle`
   {:java}

      ```javascript
      dependencies {
        classpath "com.android.tools.build:gradle:4.1.1"
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
      }
      ```
      {:codeblock}
      {:java}

   - Add `kotlin-android` plugin to the App level `build.gradle`
   {:java}

      ```javascript
      plugins {
         id 'com.android.application'
         id 'kotlin-android'
      }
      ```
      {:codeblock}
      {:java}

1. Initialize the SDK based on the programming language used in your project.

   ```kotlin
   val appConfiguration = AppConfiguration.getInstance()

   appConfiguration.init( application,
                        AppConfiguration.REGION_US_SOUTH,
                        "guid",
                        "apikey")
   ```
   {:codeblock}
   {:kotlin}

   ```java
   AppConfiguration appConfiguration = AppConfiguration.getInstance();
   appConfiguration.init(getApplication(), AppConfiguration.REGION_US_SOUTH, "guid", "apikey");
   ```
   {:codeblock}
   {:java}

   where,
   - `region` - Region name where the service instance is created. For example, `AppConfiguration.REGION_US_SOUTH`.
   - `guid` - Instance Id of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the dashboard.
   - `apikey` - ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the dashboard.

1. Set the `collectionId` for feature fetching operation.

   ```kotlin
   appConfiguration.setCollectionId("collectionId")
   ```
   {:codeblock}
   {:kotlin}

   ```java
   appConfiguration.setCollectionId("collectionId");
   ```
   {:codeblock}
   {:java}

   where, `collectionId` is the Id of the collection created in {{site.data.keyword.appconfig_short}} service instance.

1. Set client attributes for feature evaluation.

   ```kotlin
   JSONObject attributes = new JSONObject();
   try {

       attributes.put("cityRadius", "40");
       attributes.put("radius", "50");
       attributes.put("city", "Bengaluru"); 
       attributes.put("country", "India");

   } catch (JSONException e) {
       e.printStackTrace();
   }

   appConfiguration.setClientAttributes(attributes)
   ```
   {:codeblock}
   {:kotlin}

   ```java
   JSONObject attributes = new JSONObject();

   try {
       attributes.put("cityRadius", "40");
       attributes.put("radius", "50");
       attributes.put("city", "Bengaluru"); 
       attributes.put("country", "India");
   } catch (JSONException e) {
       e.printStackTrace();
   }

   appConfiguration.setClientAttributes(attributes);
   ```
   {:codeblock}
   {:java}

1. Listen to the feature changes

   ```kotlin
   appConfiguration.registerFeaturesUpdateListener(object : FeaturesUpdateListener {

       override fun onFeaturesUpdate() {
           // ADD YOUR CODE
       }
   })
   ```
   {:codeblock}
   {:kotlin}

   ```java
   appConfiguration.registerFeaturesUpdateListener(new FeaturesUpdateListener() {
       @Override
       public void onFeaturesUpdate() {
          // ADD YOUR CODE
       }
   });
   ```
   {:codeblock}
   {:java}

1. Enable or disable logger. By default, it is set to disable.

   ```kotlin
   val appConfiguration = AppConfiguration.getInstance()

   // Enable Logger 

   appConfiguration.enableDebug(true)

   // Disable Logger

   appConfiguration.enableDebug(false)
   ```
   {:codeblock}
   {:kotlin}

   ```java
   AppConfiguration appConfiguration = AppConfiguration.getInstance();

   // Enable Logger 
   appConfiguration.enableDebug(true);

   // Disable Logger
   appConfiguration.enableDebug(false);
   ```
   {:codeblock}
   {:java}

### Examples for using feature related APIs
{: #ac-integrate-ff-example-android}

Refer to the below examples for using the feature related APIs.

#### Get all features
{: #ac-integrate-ff-get-all-features-android}

```kotlin
val features: HashMap<String, Feature>? = appConfiguration.getFeatures();
```
{:codeblock}
{:kotlin}

```java
HashMap<String,Feature> features =  appConfiguration.getFeatures();
```
{:codeblock}
{:java}

#### Get single feature
{: #ac-integrate-ff-get-single-feature-android}

```kotlin
val feature: Feature? = appConfiguration.getFeature("featureId")
```
{:codeblock}
{:kotlin}

```java
Feature feature = appConfiguration.getFeature("featureId");
```
{:codeblock}
{:java}

#### Feature evaluation
{: #ac-integrate-ff-feature-evaluation-android}

```kotlin
val appConfiguration = AppConfiguration.getInstance()
val feature: Feature? = appConfiguration.getFeature("featureId")

if (feature?.getFeatureDataType() === Feature.FeatureType.NUMERIC) {

    val value = feature.getCurrentValue<Int>()

} else if (feature?.getFeatureDataType() === Feature.FeatureType.BOOLEAN) {

    val value = feature.getCurrentValue<Boolean>()

} else if (feature?.getFeatureDataType() === Feature.FeatureType.STRING) {

    val value = feature.getCurrentValue<String>()

}
```
{:codeblock}
{:kotlin}

```java
AppConfiguration appConfiguration = AppConfiguration.getInstance();
Feature feature = appConfiguration.getFeature("featureId")
if(feature != null) 
    switch (feature.getFeatureDataType())
        case STRING:
            String value = (String) feature.getCurrentValue();
            System.out.println(value);
            break;
        case BOOLEAN:
            Boolean boolVal = (Boolean) feature.getCurrentValue();
            System.out.println(boolVal);
            break;
        case NUMERIC:
            Integer intVal = (Integer) feature.getCurrentValue();
            System.out.println(intVal);
            break;
    }
}
```
{:codeblock}
{:java}

