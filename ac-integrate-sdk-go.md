---

copyright:
  years: 2021
lastupdated: "2021-02-21"

keywords: app-configuration, app configuration, integrate sdk, go sdk, go language, go

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

# App Configuration server SDK for Go
{: #ac-golang}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Golang web and mobile applications, microservices, and distributed environments. 
{:shortdesc}

## Integrating server SDK for Go
{: #ac-integrate-golang-sdk}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Golang web and mobile applications, microservices, and distributed environments. You can evaluate the values of your feature flag by integrating the {{site.data.keyword.appconfig_short}} SDK. 

1. Install the SDK using the following code from the `git` repository.

   ```sh
   go get -u github.com/IBM/appconfiguration-go-sdk
   ```
   {: codeblock}

1. In your Golang microservice or application, include the SDK module with: 

   ```javascript
   import AppConfiguration "github.com/IBM/appconfiguration-go-sdk/lib"
   ```
   {: codeblock}

1. Initialize the SDK to connect with your {{site.data.keyword.appconfig_short}} service instance.
   {: #ac-init-golang-sdk}

   ```javascript
   appConfiguration = AppConfiguration.GetInstance()
   appConfiguration.Init("region", "guid", "apikey")

   // Set the collection Id
   appConfiguration.SetCollectionId("collectionId")
   ```
   {: codeblock}

   where,
   - region: Region name where the service instance is created. Use `AppConfiguration.REGION_US_SOUTH` for Dallas and `AppConfiguration.REGION_EU_GB` for London.
   - guid: Instance Id of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - apiKey: ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - collectionId: Id of the collection created in {{site.data.keyword.appconfig_short}} service instance.

   By default, live features update from the server is enabled. To turn off live features update, see [feature operations](#ac-golang-example).
   {: note}

1. *Optional*: You can work offline with local feature file and perform [feature operations](#ac-golang-example). After setting the `collectionId`, follow the below step:

   ```javascript
   appConfiguration.FetchFromFeatureFile( "featureFilePath", "liveFeatureUpdateEnabled")
   ```
   {: codeblock}

   where,
   - featureFilePath: Path to the JSON file which contains feature details and segment details.
   - liveFeatureUpdateEnabled: Set this value to `false` if the new feature values shouldn't be fetched from the server. Make sure to provide a proper JSON file in the `featureFilePath`. By default, this value is enabled.

### Examples for using feature related APIs
{: #ac-golang-example}

Refer to the below examples for using the feature related APIs.

#### Get single feature
{: #ac-golang-get-single-feature}

```javascript
feature := appConfiguration.GetFeature("featureId")

if(feature.IsEnabled()) {
        // enable feature
} else {
        // disable the feature
}
fmt.Println(feature);
fmt.Println("Feature Name %s", feature.GetFeatureName());
fmt.Println("Feature Id  %s", feature.GetFeatureId());
fmt.Println("Feature Type %s", feature.GetFeatureDataType());
fmt.Println("Feature is enabled %t ", feature.IsEnabled());
```
{: codeblock}

#### Get all features
{: #ac-golang-get-all-features}

```javascript
features := appConfiguration.GetFeatures()

feature := features["featureId"];

fmt.Println("Feature Name %s", feature.GetFeatureName());
fmt.Println("Feature Id  %s", feature.GetFeatureId());
fmt.Println("Feature Type %s", feature.GetFeatureDataType());
fmt.Println("Feature is enabled %t ", feature.IsEnabled());
```
{: codeblock}

#### Feature evaluation
{: #ac-golang-feature-evaluation}

You can use the `feature.GetCurrentValue(identityId, identityAttributes)` method to evaluate the value of the feature flag. You should pass an unique `identityId` as the parameter to perform the feature flag evaluation. If the feature flag is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a map.

```javascript
identityId := "identityId"
identityAttributes := make(map[string]interface{})
identityAttributes["city"] = "Bangalore"
identityAttributes["country"] = "India"

featureVal := feature.GetCurrentValue(identityId, identityAttributes)
```
{: codeblock}

#### Listen to the feature changes
{: #ac-golang-listen-feature-changes}

To listen to the data changes, add the following code in your application:

```javascript
appConfiguration.RegisterFeaturesUpdateListener(func() {
    fmt.Println("Get your feature value now ")
})
```
{: codeblock}

#### Fetch latest data
{: #ac-golang-fetch-latest-data}

```javascript
appConfiguration.FetchFeatureData()
```
{: codeblock}