---

copyright:
  years: 2021
lastupdated: "2021-03-03"

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
{:shortdesc}

## Integrating server SDK for Java
{: #ac-integrate-java-sdk}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Java applications. You can evaluate the values of your feature flag by integrating the {{site.data.keyword.appconfig_short}} SDK. 

1. Install the SDK using one of the following ways.

   - Using **Maven**:

      ```xml
      <dependency>
         <groupId>com.ibm.cloud</groupId>
         <artifactId>appconfiguration-java-sdk</artifactId>
         <version>1.0.0</version>
      </dependency>
      ```
      {: codeblock}

   - Get the package through **Gradle** by adding the following:

      ```sh
      implementation group: 'com.ibm.cloud', name: 'appconfiguration-java-sdk', version: '1.0.0'
      ```
      {: codeblock}

1. In your Java microservice or application, include the SDK with: 

   ```javascript
   import com.ibm.cloud.appconfiguration.sdk.AppConfiguration
   ```
   {: codeblock}

1. Initialize the SDK to connect with your {{site.data.keyword.appconfig_short}} service instance.
   {: #ac-init-java-sdk}

   ```javascript
   AppConfiguration appConfiguration = AppConfiguration.getInstance();
   appConfiguration.init('region','guid','apikey');

   // Set the Collection ID
   appConfiguration.setCollectionId('collectionId');
   ```
   {: codeblock}

   where,
   - region: Region name where the service instance is created. Use `AppConfiguration.REGION_US_SOUTH` for Dallas and `AppConfiguration.REGION_EU_GB` for London.
   - guid: Instance Id of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - apiKey: ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - collectionId: Id of the collection created in {{site.data.keyword.appconfig_short}} service instance.

1. *Optional*: You can work offline with local feature file and perform [feature operations](#ac-java-example). After setting the `collectionId`, follow the below step:

   ```javascript
   appConfiguration.fetchFeaturesFromFile('featureFilePath', liveFeatureUpdateEnabled);
   ```
   {: codeblock}

   where,
   - featureFilePath: Path to the JSON file which contains feature details and segment details.
   - liveFeatureUpdateEnabled: Set this value to `false` if the new feature values shouldn't be fetched from the server. Make sure to provide a proper JSON file in the `featureFilePath` path. By default, this value is enabled.

### Examples for using feature related APIs
{: #ac-java-example}

Refer to the below examples for using the feature related APIs.

#### Get single feature
{: #ac-java-get-single-feature}

```java
Feature feature = appConfiguration.getFeature("feature_id");

if (feature) {
   if (feature.isEnabled()) {
      // enable feature
   }
   else {
      // disable the feature
   }

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

Feature feature = features.get("feature_id");

if (feature) {
   System.out.println("Feature Name : " + feature.getFeatureName());
   System.out.println("Feature Id : " + feature.getFeatureId());
   System.out.println("Feature Type : " + feature.getFeatureDataType());
   System.out.println("Feature is enabled : " + feature.isEnabled());
}
```
{: codeblock}

#### Feature evaluation
{: #ac-java-feature-evaluation}

You can use the `feature.getCurrentValue(identityId, identityAttributes)` method to evaluate the value of the feature flag. You should pass an unique `identityId` as the parameter to perform the feature flag evaluation. If the feature flag is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a JSONObject.

```json
JSONObject identityAttributes = new JSONObject();
identityAttributes.put("city", "Bangalore");
identityAttributes.put("country", "India");

String value = (String) feature.getCurrentValue("identityId", identityAttributes);
```
{: codeblock}

#### Listen to the feature changes
{: #ac-java-listen-feature-changes}

To listen to the data changes, add the following code in your application:

```java
appConfiguration.registerFeaturesUpdateListener(new FeaturesUpdateListener() {
    @Override
    public void onFeaturesUpdate() {
       System.out.println("Got feature now");
    }
});
```
{: codeblock}

#### Fetch latest data
{: #ac-java-fetch-latest-data}

```java
appConfiguration.fetchFeatureData();
```
{: codeblock}
