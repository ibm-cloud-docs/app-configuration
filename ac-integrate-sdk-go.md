---

copyright:
  years: 2021
lastupdated: "2021-09-09"

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
{: shortdesc}

## Integrating server SDK for Go
{: #ac-integrate-golang-sdk}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Golang web and mobile applications, microservices, and distributed environments. You can evaluate the values of your property and feature flag by integrating the {{site.data.keyword.appconfig_short}} SDK.

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

   appConfiguration.SetContext("collectionId", "environmentId")
   ```
   {: codeblock}

   where,
   - region: Region name where the service instance is created. Use `AppConfiguration.REGION_US_SOUTH` for Dallas, `AppConfiguration.REGION_EU_GB` for London, and `AppConfiguration.REGION_AU_SYD` for Sydney.
   - guid: Instance Id of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - apiKey: ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - collectionId: Id of the collection created in {{site.data.keyword.appconfig_short}} service instance.
   - environmentId: Id of the environment created in App Configuration service instance under the Environments section.

1. *Optional*: You can work [offline](/docs/app-configuration?topic=app-configuration-ac-offline) with local configuration file and perform [feature and property operations](#ac-golang-example).

After `appConfiguration.Init("region", "guid", "apikey")`, follow the below steps:

   ```javascript
  appConfiguration.SetContext("collectionId", "environmentId", AppConfiguration.ContextOptions{
  ConfigurationFile: "path/to/configuration/file.json",
  LiveConfigUpdateEnabled: false,
})
   ```
   {: codeblock}

   where,
   - ConfigurationFile: Path to the JSON file, which contains configuration details.
   - LiveConfigUpdateEnabled: Set this value to `false` if the new configuration values shouldn't be fetched from the server. Make sure to provide a proper JSON file in the `ConfigurationFile`. By default, this value is enabled.

### Examples for using property and feature related APIs
{: #ac-golang-example}

Refer to the below examples for using the property and feature related APIs.

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

You can use the `feature.GetCurrentValue(entityId, entityAttributes)` method to evaluate the value of the feature flag. You should pass an unique `entityId` as the parameter to perform the feature flag evaluation. If the feature flag is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a map.

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

You can use the `property.GetCurrentValue(entityId, entityAttributes)` method to evaluate the value of the property. You should pass an unique `entityId` as the parameter to perform the property evaluation. If the property is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a map.

```javascript
entityId := "entityId"
entityAttributes := make(map[string]interface{})
entityAttributes["email"] = "ibm.com"
entityAttributes["city"] = "Bengaluru"

propertyVal := property.GetCurrentValue(entityId, entityAttributes)
```
{: codeblock}

## Supported Data types
{: #ac-integrate-go-supported-data-types}

{{site.data.keyword.appconfig_short}} service allows to configure the feature flag and properties in the following data types: Boolean,
Numeric, String. The String data type can be a text string , JSON or YAML. The SDK processes each
format accordingly as shown in the below table.

| **Feature or Property value**                                                                                      | **DataType** | **DataFormat** | **Type of data returned <br> by `GetCurrentValue()`** | **Example output**                                                   |
| ------------------------------------------------------------------------------------------------------------------ | ------------ | -------------- | ----------------------------------------------------- | -------------------------------------------------------------------- |
| `true`                                                                                                             | BOOLEAN      | not applicable | `bool`                                                | `true`                                                               |
| `25`                                                                                                               | NUMERIC      | not applicable | `float64`                                             | `25`                                                                 |
| "a string text"                                                                                                    | STRING       | TEXT           | `string`                                              | `a string text`                                                      |
| <pre>{<br>  "firefox": {<br>    "name": "Firefox",<br>    "pref_url": "about:config"<br>  }<br>}</pre> | STRING       | JSON           | `map[string]interface{}`                              | `map[browsers:map[firefox:map[name:Firefox pref_url:about:config]]]` |
| <pre>men:<br>  - John Smith<br>  - Bill Jones<br>women:<br>  - Mary Smith<br>  - Susan Williams</pre>  | STRING       | YAML           | `map[string]interface{}`                              | `map[men:[John Smith Bill Jones] women:[Mary Smith Susan Williams]]` |

  #### Feature flag

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

#### Listen to the property and feature changes


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
