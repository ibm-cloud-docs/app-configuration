---

copyright:
  years: 2021
lastupdated: "2021-02-10"

keywords: app-configuration, app configuration, integrate sdk, android sdk, android, kotlin, java

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

# App Configuration client SDK for Android
{: #ac-integrate-sdks-android}

{{site.data.keyword.appconfig_short}} service provides Android client SDK to integrate with your Android application written in Kotlin or Java programming language. 
{:shortdesc}

## Prerequisites
{: #ac-integrate-ff-sdk-android-prereqs}

Following are the prerequisites for using the {{site.data.keyword.appconfig_short}} service SDK for Android:

- Android API level 22 or later
- [Android Studio](https://developer.android.com/studio/index.html){:external}
- [Gradle](https://gradle.org/install){:external}

## Integrating client SDK for Android app written in Kotlin
{: #ac-integrate-ff-sdk-android-kotlin}

{{site.data.keyword.appconfig_short}} service provides Android client SDK to integrate with your Android application. You can evaluate the values of your feature flag by integrating the SDK. 

1. Install the SDK using either one of the following option:
   - [Download](https://github.com/IBM/appconfiguration-android-client-sdk) and import the package to your Android studio project.
   - Get the package through Gradle by adding the following:
      - Add {{site.data.keyword.appconfig_short}} Android client SDK dependency to Project level `build.gradle` file.

         ```javascript
         repositories {
            jcenter()
         }
         ```
         {:codeblock}
   
      - Add {{site.data.keyword.appconfig_short}} Android client SDK dependency to Module level `build.gradle` file.

         ```javascript
         dependencies {
            implementation "com.ibm.appconfiguration.android:lib:1.1.0"
         }
         ```
         {:codeblock}

1. Configure the `AndroidManifest.xml` file for Internet permission.

   ```xml
   <uses-permission android:name="android.permission.INTERNET"/>
   ```
   {:codeblock}

1. Initialize the SDK.

   ```kotlin
   val appConfiguration = AppConfiguration.getInstance()

   appConfiguration.init( application,
                         AppConfiguration.REGION_US_SOUTH,
                         "guid",
                         "apikey")

   //To start the feature fetching operation, set the collection_id in the following way.
   appConfiguration.setCollectionId("collection_id")
   ```
   {:codeblock}

   where,
   - `region` - Region name where the service instance is created. For example, `AppConfiguration.REGION_US_SOUTH`.
   - `guid` - GUID of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the dashboard.
   - `apikey` - ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the dashboard.
   - `collection_id` - Id of the collection created in {{site.data.keyword.appconfig_short}} service instance.

1. Listen to the feature changes

   ```kotlin
   appConfiguration.registerFeaturesUpdateListener(object : FeaturesUpdateListener {

       override fun onFeaturesUpdate() {
           // ADD YOUR CODE
       }
   })
   ```
   {:codeblock}

### Examples for using feature related APIs for Android app written in Kotlin
{: #ac-integrate-ff-example-android-kotlin}

Refer to the below examples for using the feature related APIs.

- **Get single feature**

   ```kotlin
   val feature: Feature? = appConfiguration.getFeature("featureId")
   ```
   {:codeblock}

- **Get all features**

   ```kotlin
   val features: HashMap<String, Feature>? = appConfiguration.getFeatures();
   ```
   {:codeblock}

- **Feature evaluation**

   You can use the `feature.getCurrentValue()` method to evaluate the value of the feature flag. You should pass an unique `identityId` as the parameter to perform the feature flag evaluation. If the feature flag is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a *JSONObject*.

   ```kotlin
   JSONObject identityAttributes = new JSONObject(); 
   try { 
   	identityAttributes.put("city", "Bangalore"); 
   	identityAttributes.put("country", "India"); 
   } catch (JSONException e) { 
   	e.printStackTrace(); 
   }

   val feature: Feature? = appConfiguration.getFeature("featureId") 
   if (feature?.getFeatureDataType() === Feature.FeatureType.NUMERIC) { 
   	val value = feature.getCurrentValue("identityId", identityAttributes) 
   } else if (feature?.getFeatureDataType() === Feature.FeatureType.BOOLEAN) { 
   	val value = feature.getCurrentValue("identityId", identityAttributes) 
   } else if (feature?.getFeatureDataType() === Feature.FeatureType.STRING) { 
   	val value = feature.getCurrentValue("identityId", identityAttributes) 
   }
   ```
   {:codeblock}

- Force fetch the features from server.
   ```kotlin
   appConfiguration.fetchFeatureData()
   ```
   {:codeblock}

## Integrating client SDK for Android app written in Java
{: #ac-integrate-ff-sdk-android-java}

{{site.data.keyword.appconfig_short}} service provides Android client SDK to integrate with your Android application. You can evaluate the values of your feature flag by integrating the SDK. 

1. Install the SDK using either one of the following option:
   - [Download](https://github.com/IBM/appconfiguration-android-client-sdk) and import the package to your Android studio project.
   - Get the package through Gradle by adding the following:
      - Add {{site.data.keyword.appconfig_short}} Android client SDK dependency to Project level `build.gradle` file.

         ```javascript
         repositories {
            jcenter()
         }
         ```
         {:codeblock}
   
      - Add {{site.data.keyword.appconfig_short}} Android client SDK dependency to Module level `build.gradle` file.

         ```javascript
         dependencies {
            implementation "com.ibm.appconfiguration.android:lib:1.1.0"
         }
         ```
         {:codeblock}

1. Configure the `AndroidManifest.xml` file for Internet permission.

   ```xml
   <uses-permission android:name="android.permission.INTERNET"/>
   ```
   {:codeblock}

1. Integrate Kotlin to your Java project with these steps:

   - Add the Kotlin gradle plugin to the Module level `build.gradle`

      ```javascript
      dependencies {
        classpath "com.android.tools.build:gradle:4.1.1"
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
      }
      ```
      {:codeblock}

   - Add `kotlin-android` plugin to the App level `build.gradle`

      ```javascript
      plugins {
         id 'com.android.application'
         id 'kotlin-android'
      }
      ```
      {:codeblock}

1. Initialize the SDK.

   ```java
   AppConfiguration appConfiguration = AppConfiguration.getInstance();
   appConfiguration.init(getApplication(), AppConfiguration.REGION_US_SOUTH, "guid", "apikey");

   // To start the feature fetching operation, set the collection_id in the following way.
   appConfiguration.setCollectionId("collection_id");
   ```
   {:codeblock}

   where,
   - `region` - Region name where the service instance is created. For example, `AppConfiguration.REGION_US_SOUTH`.
   - `guid` - GUID of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the dashboard.
   - `apikey` - ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the dashboard.
   - `collection_id` - Id of the collection created in {{site.data.keyword.appconfig_short}} service instance.

1. Listen to the feature changes

   ```java
   appConfiguration.registerFeaturesUpdateListener(new FeaturesUpdateListener() {
       @Override
       public void onFeaturesUpdate() {
          // ADD YOUR CODE
       }
   });
   ```
   {:codeblock}

### Examples for using feature related APIs for Android app written in Java
{: #ac-integrate-ff-example-android-java}

Refer to the below examples for using the feature related APIs.

- **Get single feature**

   ```java
   Feature feature = appConfiguration.getFeature("featureId");
   ```
   {:codeblock}

- **Get all features**

   ```java
   HashMap<String,Feature> features =  appConfiguration.getFeatures();
   ```
   {:codeblock}

- **Feature evaluation**

   You can use the `feature.getCurrentValue()` method to evaluate the value of the feature flag. You should pass an unique `identityId` as the parameter to perform the feature flag evaluation. If the feature flag is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a *JSONObject*.

   ```java
   JSONObject identityAttributes = new JSONObject(); 
   try { 
   	identityAttributes.put("city", "Bengaluru"); 
   	identityAttributes.put("country", "India"); 
   } catch (JSONException e) { 
   	e.printStackTrace(); 
   } 

   Feature feature = appConfiguration.getFeature("featureId") 
   if(feature != null) {
   	switch (feature.getFeatureDataType()) {
   		case STRING: 
   			String value = (String) feature.getCurrentValue("identityId", identityAttributes); 						 
                           System.out.println(value); 
   			break; 	
   		case BOOLEAN: 
   			Boolean boolVal = (Boolean) feature.getCurrentValue("identityId", identityAttributes);
                           System.out.println(boolVal); 
   			break; 
   		case NUMERIC: 
   			Integer intVal = (Integer) feature.getCurrentValue("identityId", identityAttributes); 					
                            System.out.println(intVal); 
   			break;
   	 } 
   }
   ```
   {:codeblock}

- Force fetch the features from server.
   ```java
   appConfiguration.fetchFeatureData()
   ```
   {:codeblock}
