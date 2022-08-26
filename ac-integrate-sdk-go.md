---

copyright:
  years: 2021, 2022
lastupdated: "2022-08-26"

keywords: app-configuration, app configuration, integrate sdk, go sdk, go language, go

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# App Configuration server SDK for Go
{: #ac-golang}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Golang web and mobile applications, microservices, and distributed environments.
{: shortdesc}

## Prerequisites
{: #ac-integrate-golang-sdk-prereqs}

Following is the prerequisite for using {{site.data.keyword.appconfig_short}} service SDK for Go:

- Go version 1.16 or later

## Integrating server SDK for Go
{: #ac-integrate-golang-sdk}

The v1.x.x versions of the {{site.data.keyword.appconfig_short}} Go SDK have been retracted.
{: note}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Golang web and mobile applications, microservices, and distributed environments. You can evaluate the values of your property and feature flag by integrating the {{site.data.keyword.appconfig_short}} SDK.

1. Install the SDK by using the following code from the `git` repository.

   ```sh
   go get -u github.com/IBM/appconfiguration-go-sdk@latest
   ```
   {: codeblock}

1. In your Golang microservice or application, include the SDK module with:

   ```javascript
   import (
      AppConfiguration "github.com/IBM/appconfiguration-go-sdk/lib"
   )
   ```
   {: codeblock}

   Run `go mod tidy` to download and install the new dependency and update your Go application's `go.mod` file.

1. Initialize the SDK to connect with your {{site.data.keyword.appconfig_short}} service instance.
   {: #ac-init-golang-sdk}

   ```javascript
   appConfiguration = AppConfiguration.GetInstance()
   appConfiguration.Init("region", "guid", "apikey")
   appConfiguration.SetContext("collectionId", "environmentId")
   ```
   {: codeblock}

   Where,
   - `Region`: Region name where the service instance is created. Use `AppConfiguration.REGION_US_SOUTH` for Dallas, `AppConfiguration.REGION_US_EAST` for Washington DC, `AppConfiguration.REGION_EU_GB` for London, and `AppConfiguration.REGION_AU_SYD` for Sydney.
   - `guid`: Instance ID of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - `apiKey`: ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - `collectionId`: ID of the collection created in {{site.data.keyword.appconfig_short}} service instance.
   - `environmentId`: ID of the environment created in App Configuration service instance under the Environments section.

   The `Init()` and `SetContext()` are the initialisation methods and should be invoked only once using `appConfigClient`. The `appConfigClient`, once initialized, can be obtained across modules using `AppConfiguration.GetInstance()`.
   {: important}

### Option to use a persistent cache for configuration
{: #ac-go-persistent-cache}

For your application and SDK to continue operations even during the unlikely scenario of an {{site.data.keyword.appconfig_short}} service downtime, across your application restarts, you can configure the SDK to work by using a persistent cache. The SDK uses the persistent cache to store the {{site.data.keyword.appconfig_short}} data that is available across your application restarts.

```go
// 1. default (without persistent cache)
appConfiguration.SetContext(collectionId, environmentId)
// 2. with persistent cache
appConfiguration.SetContext(collectionId, environmentId, AppConfiguration.ContextOptions{
   PersistentCacheDirectory: "/var/lib/docker/volumes/",
})
```
{: codeblock}

Where `persistentCacheDirectory`: Absolute path to a directory that has read and write permission for the user. The SDK creates a file `AppConfiguration.json` in the specified directory, and it is used as the persistent cache to store the {{site.data.keyword.appconfig_short}} service information.

When persistent cache is enabled, the SDK keeps the last known good configuration at the persistent cache. If the {{site.data.keyword.appconfig_short}} server is unreachable, the latest configurations at the persistent cache are loaded to the application to continue working.

Ensure that the cache file is not lost or deleted in any case. For example, consider the case when a kubernetes pod is restarted and the cache file (`appconfiguration.json`) was stored in ephemeral volume of the pod. As pod gets restarted, kubernetes destroys the ephermal volume in the pod, as a result the cache file gets deleted. So, make sure that the cache file created by the SDK is always stored in persistent volume by providing the correct absolute path of the persistent directory.
{: important}

### Offline options
{: #ac-go-offline}

The SDK is also designed to serve configurations, and perform feature flag and property evaluations without being connected to {{site.data.keyword.appconfig_short}} service.

```go
appConfiguration.SetContext(collectionId, environmentId, AppConfiguration.ContextOptions{
   BootstrapFile: "saflights/flights.json",
   LiveConfigUpdateEnabled: false,
})
```
{: codeblock}

Where,

- `BootstrapFile`: Absolute path of the JSON file, which contains configuration details. Make sure to provide a proper JSON file. You can generate this file by using `ibmcloud ac config` command of the {{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_short}} CLI.

- `LiveConfigUpdateEnabled`: Live configuration update from the server. Set this value to `false` if the new configuration values must not be fetched from the server. By default, this value is enabled.

### Examples for using property and feature-related APIs
{: #ac-golang-example}

Refer to the listed examples for using the property and feature-related APIs.

#### Get single feature
{: #ac-golang-get-single-feature}

```javascript
feature, err := appConfigClient.GetFeature("featureId")
if err == nil {
   fmt.Println("Feature Name", feature.GetFeatureName())
   fmt.Println("Feature Id", feature.GetFeatureID())
   fmt.Println("Feature Type", feature.GetFeatureDataType())

   if (feature.IsEnabled()) {
      // feature flag is enabled
   } else {
      // feature flag is disabled
   }
}
```
{: codeblock}

#### Get all features
{: #ac-golang-get-all-features}

```javascript
features, err := appConfigClient.GetFeatures()
if err == nil {
   feature := features["featureId"]
    
   fmt.Println("Feature Name", feature.GetFeatureName())
   fmt.Println("Feature Id", feature.GetFeatureID())
   fmt.Println("Feature Type", feature.GetFeatureDataType())
   fmt.Println("Is feature enabled?", feature.IsEnabled())
}
```
{: codeblock}

#### Feature evaluation
{: #ac-golang-feature-evaluation}

You can use the `feature.GetCurrentValue(entityId, entityAttributes)` method to evaluate the value of the feature flag. `GetCurrentValue` returns one of the *Enabled/Disabled/Overridden* value based on the evaluation.

```javascript
entityId := "john_doe"
entityAttributes := make(map[string]interface{})
entityAttributes["city"] = "Bangalore"
entityAttributes["country"] = "India"

featureVal := feature.GetCurrentValue(entityId, entityAttributes)
```
{: codeblock}

Where,

- `entityId`: a string identifier related to the `Entity` against which the feature will be evaluated. For example, an entity might be an instance of an application that runs on a mobile device, a microservice that runs on the {{site.data.keyword.cloud_notm}}, or a component of infrastructure that runs that microservice. For any entity to interact with {{site.data.keyword.appconfig_short}}, it must provide a unique `entity ID`.

- `entityAttributes`: `entityAttributes` is a map of type `map[string]interface{}` consisting of the attribute name and their values that defines the specified entity. This is an optional parameter if the feature flag is not configured with any targeting definition. If the targeting is configured, then `entityAttributes` should be provided for the rule evaluation. An attribute is a parameter that is used to define a segment. The SDK uses the attribute values to determine if the specified entity satisfies the targeting rules, and returns the appropriate feature flag value.

#### Get single property
{: #ac-golang-get-single-property}

```javascript
property, err := appConfigClient.GetProperty("propertyId")
if err == nil {
   fmt.Println("Property Name", property.GetPropertyName())
   fmt.Println("Property Id", property.GetPropertyID())
   fmt.Println("Property Type", property.GetPropertyDataType())
}
```
{: codeblock}

#### Get all properties
{: #ac-golang-get-all-properties}

```javascript
properties, err := appConfigClient.GetProperties()
if err == nil {
   property := properties["propertyId"]
    
   fmt.Println("Property Name", property.GetPropertyName())
   fmt.Println("Property Id", property.GetPropertyID())
   fmt.Println("Property Type", property.GetPropertyDataType())
}
```
{: codeblock}

#### Property evaluation
{: #ac-golang-property-evaluation}

You can use the `property.GetCurrentValue(entityId, entityAttributes)` method to evaluate the value of the property. `GetCurrentValue` returns the default property value or its overridden value based on the evaluation.

```javascript
entityId := "entityId"
entityAttributes := make(map[string]interface{})
entityAttributes["city"] = "Bengaluru"
entityAttributes["country"] = "India"

propertyVal := property.GetCurrentValue(entityId, entityAttributes)
```
{: codeblock}

Where,

- `entityId`: `entityId` is a string identifier related to the Entity against which the property will be evaluated. For example, an entity might be an instance of an application that runs on a mobile device, a microservice that runs on the cloud, or a component of infrastructure that runs that microservice. For any entity to interact with {{site.data.keyword.appconfig_short}}, it must provide a unique `entity ID`.

- `entityAttributes`: `entityAttributes` is a map of type `map[string]interface{}` consisting of the attribute name and their values that defines the specified entity. This is an optional parameter if the property is not configured with any targeting definition. If the targeting is configured, then `entityAttributes` should be provided for the rule evaluation. An attribute is a parameter that is used to define a segment. The SDK uses the attribute values to determine if the specified entity satisfies the targeting rules, and returns the appropriate property value.

### Get secret property
{: #ac-integrate-go-get-secret-property}

```javascript
secretPropertyObject, err := appConfiguration.GetSecret(propertyID, secretsManagerObject)
```
{: codeblock}

Where,

- `propertyID`: `propertyID` is the unique string identifier, using this you will be able to fetch the property that will provide the necessary data to fetch the secret.

- `secretsManagerObject`: `secretsManagerObject` is a {{site.data.keyword.secrets-manager_short}} variable or object which will be used for getting the secrets during the secret property evaluation. For more information on how to create a {{site.data.keyword.secrets-manager_short}} object refer [here](https://cloud.ibm.com/apidocs/secrets-manager?code=go).

#### Evaluate a secret property
{: #ac-integrate-go-evaluate-secret-property}

Use the `secretPropertyObject.GetCurrentValue(entityId, entityAttributes)` method to evaluate the value of the secret property. `GetCurrentValue` returns the secret value based on the evaluation.

```javascript
entityId := "john_doe"
entityAttributes := make(map[string]interface{})
entityAttributes["city"] = "Bangalore"
entityAttributes["country"] = "India"

getSecretRes, detailedResponse, err := secretPropertyObject.GetCurrentValue(entityId, entityAttributes)
```
{: codeblock}

Where,

- `entityId`: `entityId` is a string identifier related to the Entity against which the property will be evaluated. For example, an entity might be an instance of an app that runs on a mobile device, a microservice that runs on the cloud, or a component of infrastructure that runs that microservice. For any entity to interact with {{site.data.keyword.appconfig_short}}, it must provide a unique entity ID.

- `entityAttributes`: `entityAttributes` is a map of type `map[string]interface{}` consisting of the attribute name and their values that defines the specified entity. This is an optional parameter if the property is not configured with any targeting definition. If the targeting is configured, then `entityAttributes` should be provided for the rule evaluation. An attribute is a parameter that is used to define a segment. The SDK uses the attribute values to determine if the specified entity satisfies the targeting rules, and returns the appropriate value.

#### How to access the payload secret data from the response
{: #ac-integrate-go-access-payload-secret-data}

Add the following import statement: 

```javascript
//make sure this import statement is added
import (sm "github.com/IBM/secrets-manager-go-sdk/secretsmanagerv1")

secret := getSecretRes.Resources[0].(*sm.SecretResource)
secretData := secret.SecretData.(map[string]interface{})
payload := secretData["payload"]
```
{: codeblock}

The `GetCurrentValue` will be sending the three objects as part of response.

- `getSecretRes`: This will give the meta data and payload.
- `detailedResponse`: This will give entire data which includes the http response header data, meta data, and payload.
- `err`: This will give the error response if the request is invalid or failed for some reason.

`secretData["payload"]` will return `interface{}` so based on the data you need to do the type casting.
{: note}

### Fetching the appConfigClient across other modules
{: #ac-integrate-go-fetch-appconfigclient}

Once the SDK is initialized, the `appConfigClient` can be obtained across other modules as shown below:

```javascript
// **other modules**

import (
   AppConfiguration "github.com/IBM/appconfiguration-go-sdk/lib"
)

appConfigClient := AppConfiguration.GetInstance()
feature, err := appConfigClient.GetFeature("online-check-in")
if (err == nil) {
   enabled := feature.IsEnabled()
   featureValue := feature.GetCurrentValue(entityId, entityAttributes)
}
```
{: codeblock}

## Supported data types
{: #ac-integrate-go-supported-data-types}

You can configure feature flags and properties with {{site.data.keyword.appconfig_short}}, supporting the following data types: Boolean, Numeric, String, and SecretRef. The String data type can be a text string, JSON, or YAML. The SDK processes each
format as shown in the table.

| **Feature or Property value** | **Data type** | **Data format** | **Type of data returned by `GetCurrentValue()`** | **Example output** |
| -- | -- | -- | -- | -- |
| `true` | BOOLEAN | not applicable | `bool` | `true` |
| `25` | NUMERIC | not applicable | `float64` | `25` |
| `{  \n  "secret_type": "kv",  \n  "id": "secret_id_data_here",  \n   "sm_instance_crn": "crn_data_added-here"  \n  }` | SECRETREF(this type is applicable only for Property) | not applicable | `map[string]interface{}` | `{  \n  "metadata": {  \n  "collection_type":"application/vnd.ibm.secrets-manager.secret+json",  \n  "collection_total": 1  \n  },  \n  "resources": [{"created_by": "iam-ServiceId-e4a2f0a4-3a76-4ebef-b2f2-fbssfddsf21",  \n  "creation_date": "2020-10-05T21:33:11Z",  \n  "crn": "crn:v1:bluemix:public:secrets-manager:us-south:a/a5eb:f1bc94a6:secret:cb7a2502-8ede",  \n  "description": "Extended description for this secret.",  \n  "expiration_date": "2021-01-01T00:00:00Z",  \n  "id": "cb7a2502-8ede-47d6-b5b6-1b7af6b6f563",  \n  "labels": ["dev","us-south"],  \n  "last_update_date": "2020-10-05T21:33:11Z",  \n  "name": "example-arbitrary-secret",  \n  "secret_data": {"payload": "secret-data"},  \n  "secret_type": "arbitrary",  \n  "state": 1,  \n  "state_description": "Active",  \n  "versions_total": 1,  \n   "versions": [{"created_by": "iam-ServiceId-222b47ab-b08e-4619-b68f-8014a2c3acb8","creation_date": "2020-11-23T20:15:01Z","id": "50277266-d706-4b3e-badb-f07257f8f581","payload_available": true,"downloaded": true}],"locks_total": 2}]  \n  }`  \n  Along with the above data we will also provide the detailed Response and error data. For more info on the response data refer [here](#ac-integrate-go-access-payload-secret-data). |
| "a string text" | STRING | TEXT | `string` | `a string text` |
| `{"firefox": {`  \n `"name": "Firefox",`  \n  `"pref_url": "about:config"`  \n }} | STRING | JSON | `map[string]interface{}` | `map[browsers:map[firefox:map[name:Firefox pref_url:about:config]]]` |
| `men:`  \n   `- John Smith`  \n   `- Bill Jones`  \n `women:`  \n   `- Mary Smith`  \n   `- Susan Williams`  | STRING | YAML | `map[string]interface{}` | `map[men:[John Smith Bill Jones] women:[Mary Smith Susan Williams]]` |
{: caption="Table 1. Example outputs" caption-side="bottom"}

### Feature flag
{: #ac-android-feat-flag}

```go
feature, err := appConfigClient.GetFeature("json-feature")
if err == nil {
  feature.GetFeatureDataType() // STRING
  feature.GetFeatureDataFormat() // JSON
  
  // Example (traversing the returned map)
  result := feature.GetCurrentValue(entityID, entityAttributes) // JSON value is returned as a Map
  result.(map[string]interface{})["key"] // returns the value of the key
}

feature, err := appConfigClient.GetFeature("yaml-feature")
if err == nil {
  feature.GetFeatureDataType() // STRING
  feature.GetFeatureDataFormat() // YAML
  
  // Example (traversing the returned map)
  result := feature.GetCurrentValue(entityID, entityAttributes) // YAML value is returned as a Map
  result.(map[string]interface{})["key"] // returns the value of the key
}
```
{: codeblock}

#### Property
{: #ac-android-property}

```go
property, err := appConfigClient.GetProperty("json-property")
if err == nil {
  property.GetPropertyDataType() // STRING
  property.GetPropertyDataFormat() // JSON

  // Example (traversing the returned map)
  result := property.GetCurrentValue(entityID, entityAttributes) // JSON value is returned as a Map
  result.(map[string]interface{})["key"] // returns the value of the key
}

property, err := appConfigClient.GetProperty("yaml-property")
if err == nil {
  property.GetPropertyDataType() // STRING
  property.GetPropertyDataFormat() // YAML

  // Example (traversing the returned map)
  result := property.GetCurrentValue(entityID, entityAttributes) // YAML value is returned as a Map
  result.(map[string]interface{})["key"] // returns the value of the key
}
```
{: codeblock}

#### Listen to the property and feature changes
{: #ac-android-listen-property}

To listen to the feature flag's or property's configuration changes, add the following code in your application. You can subscribe to configuration changes using the same `appConfigClient`.

```javascript
appConfigClient.RegisterConfigurationUpdateListener(func () {
      // **add your code**
      // To find the effect of any configuration changes, you can call the feature or property related methods

      // feature, err := appConfigClient.GetFeature("json-feature")
      // newValue := feature.GetCurrentValue(entityID, entityAttributes)
})
```
{: codeblock}

#### Fetch latest data
{: #ac-golang-fetch-latest-data}

```javascript
appConfigClient.FetchConfigurations()
```
{: codeblock}
