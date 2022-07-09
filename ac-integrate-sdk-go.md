---

copyright:
  years: 2021, 2022
lastupdated: "2022-07-08"

keywords: app-configuration, app configuration, integrate sdk, go sdk, go language, go

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# App Configuration server SDK for Go
{: #ac-golang}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Golang web and mobile applications, microservices, and distributed environments.
{: shortdesc}

## Integrating server SDK for Go
{: #ac-integrate-golang-sdk}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Golang web and mobile applications, microservices, and distributed environments. You can evaluate the values of your property and feature flag by integrating the {{site.data.keyword.appconfig_short}} SDK.

1. Install the SDK by using the following code from the `git` repository.

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

   appConfiguration.SetContext("collectionId", "environmentId")
   ```
   {: codeblock}

   Where,
   - `Region`: Region name where the service instance is created. Use `AppConfiguration.REGION_US_SOUTH` for Dallas, `AppConfiguration.REGION_US_EAST` for Washington DC, `AppConfiguration.REGION_EU_GB` for London, and `AppConfiguration.REGION_AU_SYD` for Sydney.
   - `guid`: Instance ID of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - `apiKey`: ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - `collectionId`: ID of the collection created in {{site.data.keyword.appconfig_short}} service instance.
   - `environmentId`: ID of the environment created in App Configuration service instance under the Environments section.

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

You can use the `feature.GetCurrentValue(entityId, entityAttributes)` method to evaluate the value of the feature flag. Pass a unique `entityId` as the parameter to perform the feature flag evaluation. If the feature flag is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a map.

```javascript
entityId := "entityId"
entityAttributes := make(map[string]interface{})
entityAttributes["email"] = "ibm.com"
entityAttributes["city"] = "Bengaluru"

featureVal := feature.GetCurrentValue(entityId, entityAttributes)
```
{: codeblock}

#### Get single property
{: #ac-golang-get-single-property}

```javascript
property := appConfiguration.GetProperty("propertyId")

fmt.Println(property);
fmt.Println("Property Name %s", property.GetPropertyName());
fmt.Println("Property Id  %s", property.GetPropertyId());
fmt.Println("Property Type %s", property.GetPropertyDataType());
```
{: codeblock}

#### Get all properties
{: #ac-golang-get-all-properties}

```javascript
properties := appConfiguration.GetProperties()

property := properties["propertyId"];

fmt.Println("Property Name %s", property.GetPropertyName());
fmt.Println("Property Id  %s", property.GetPropertyId());
fmt.Println("Property Type %s", property.GetPropertyDataType());
```
{: codeblock}

#### Property evaluation
{: #ac-golang-property-evaluation}

You can use the `property.GetCurrentValue(entityId, entityAttributes)` method to evaluate the value of the property. Pass a unique `entityId` as the parameter to perform the property evaluation. If the property is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a map.

```javascript
entityId := "entityId"
entityAttributes := make(map[string]interface{})
entityAttributes["email"] = "ibm.com"
entityAttributes["city"] = "Bengaluru"

propertyVal := property.GetCurrentValue(entityId, entityAttributes)
```
{: codeblock}

## Supported data types
{: #ac-integrate-go-supported-data-types}

You can configure feature flags and properties with {{site.data.keyword.appconfig_short}}, supporting the following data types: Boolean, Numeric, and String. The String data type can be a text string, JSON, or YAML. The SDK processes each
format as shown in the table.

| **Feature or Property value** | **Data type** | **Data format** | **Type of data returned by `GetCurrentValue()`** | **Example output** |
| -- | -- | -- | -- | -- |
| `true` | BOOLEAN | not applicable | `bool` | `true` |
| `25` | NUMERIC | not applicable | `float64` | `25` |
| "a string text" | STRING | TEXT | `string` | `a string text` |
| `{"firefox": {`  \n `"name": "Firefox",`  \n  `"pref_url": "about:config"`  \n }} | STRING | JSON | `map[string]interface{}` | `map[browsers:map[firefox:map[name:Firefox pref_url:about:config]]]` |
| `men:`  \n   `- John Smith`  \n   `- Bill Jones`  \n `women:`  \n   `- Mary Smith`  \n   `- Susan Williams`  | STRING | YAML | `map[string]interface{}` | `map[men:[John Smith Bill Jones] women:[Mary Smith Susan Williams]]` |
{: caption="Table 1. Example outputs" caption-side="bottom"}

### Feature flag
{: #ac-android-feat-flag}

```go
feature, err := appConfiguration.GetFeature("json-feature")
if err == nil {
    feature.GetFeatureDataType() // STRING
    feature.GetFeatureDataFormat() // JSON

    // Example (traversing the returned map)
    result := feature.GetCurrentValue(entityID, entityAttributes) // JSON value is returned as a Map
    result.(map[string]interface{})["key"] // returns the value of the key
}

feature, err := appConfiguration.GetFeature("yaml-feature")
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
property, err := appConfiguration.GetProperty("json-property")
if err == nil {
    property.GetPropertyDataType() // STRING
    property.GetPropertyDataFormat() // JSON

    // Example (traversing the returned map)
    result := property.GetCurrentValue(entityID, entityAttributes) // JSON value is returned as a Map
    result.(map[string]interface{})["key"] // returns the value of the key
}

property, err := appConfiguration.GetProperty("yaml-property")
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

To listen to the data changes, add the following code in your application:

```javascript
appConfiguration.RegisterConfigurationUpdateListener(func() {
    fmt.Println("Get your feature/property value now ")
})
```
{: codeblock}

#### Fetch latest data
{: #ac-golang-fetch-latest-data}

```javascript
appConfiguration.FetchConfigurations()
```
{: codeblock}
