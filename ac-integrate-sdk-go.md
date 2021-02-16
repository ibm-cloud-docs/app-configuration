---

copyright:
  years: 2021
lastupdated: "2021-02-16"

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

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Golang microservice or application. 
{:shortdesc}

## Integrating server SDK for Go
{: #ac-integrate-golang-sdk}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Golang microservice or application. You can evaluate the values of your feature flag by integrating the {{site.data.keyword.appconfig_short}} SDK. 

1. Install the SDK using the following code from the `git` repository.

   ```sh
   go get -u github.com/IBM/appconfiguration-sdk-go
   ```
   {: codeblock}

1. In your Golang microservice or application, include the SDK module with: 

   ```javascript
   import AppConfiguration "appconfiguration-sdk-go/lib"
   ```
   {: codeblock}

1. Initialize the SDK to connect with your {{site.data.keyword.appconfig_short}} service instance.
   {: #ac-init-golang-sdk}

   ```javascript
   appConfiguration = AppConfiguration.GetInstance()
   appConfiguration.Init(<REGION>, <GUID>, <API_KEY>)

   // initialize feature
   appConfiguration.SetCollectionId(<COLLECTION_ID>)

   // set the file or offline feature
   appConfiguration.FetchFromFeatureFile(<FEATURE_FILE_PATH>, //Add this field if liveFeatureUpdateEnabled false or get features when the device is offline during the first app load.                            
   <LIVE_FEATURE_UPDATE_ENABLED>) // This is for live update from server.
   ```
   {: codeblock}

   where,
   - REGION: Region name where the service instance is created. Use `us-south` for Dallas and `eu-gb` for London.
   - GUID: Instance Id of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - API_KEY: ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - COLLECTION_ID: Id of the collection created in {{site.data.keyword.appconfig_short}} service instance.
   - FEATURE_FILE_PATH: Path to the JSON file which contains feature details and segment details.
   - LIVE_FEATURE_UPDATE_ENABLED: Set this value to false if the new feature values shouldn't be fetched from the server. Make sure to provide a proper JSON file in the feature_file path. By default, this value is enabled.

### Examples for using feature related APIs
{: #ac-golang-example}

Refer to the below examples for using the feature related APIs.

#### Get single feature
{: #ac-golang-get-single-feature}

```javascript
feature := appConfiguration.GetFeature(<FEATURE_ID>)
```
{: codeblock}

#### Get all features
{: #ac-golang-get-all-features}

```javascript
features := appConfiguration.GetFeatures()
```
{: codeblock}

#### Feature evaluation
{: #ac-golang-feature-evaluation}

You can use the `feature.GetCurrentValue(identityId, identity)` method to evaluate the value of the feature flag. You should pass an unique `identityId` as the parameter to perform the feature flag evaluation.

```javascript
identity := make(map[string]interface{})
identity["email"] = "ibm.com"
identity["city"] = "Bengaluru"
identityId := "pvQr45"
featureVal := feature.GetCurrentValue(identityId, identity)
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
