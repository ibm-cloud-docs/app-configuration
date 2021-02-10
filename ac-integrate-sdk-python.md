---

copyright:
  years: 2020, 2021
lastupdated: "2021-02-09"

keywords: app-configuration, app configuration, integrate sdk, python sdk, python

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

# App Configuration server SDK for Python
{: #ac-python}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Python application. 
{:shortdesc}

## Integrating server SDK for Python
{: #ac-integrate-python}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Python application. You can evaluate the values of your feature flag by integrating the {{site.data.keyword.appconfig_short}} SDK. 

1. Install the SDK using either one of the following method:

   - Using `pip`

      ```
      pip install --upgrade ibm-appconfiguration-python-client-sdk
      ```
      {: codeblock}

   - Using `easy_install`

      ```
      easy_install --upgrade ibm-appconfiguration-python-client-sdk
      ```
      {: codeblock}


1. In your Python application code, include the SDK module with: 

   ```javascript
   from ibm_appconfiguration import AppConfiguration, Feature, FeatureType
   ```
   {: codeblock}

1. Initialize the sdk to connect with your {{site.data.keyword.appconfig_short}} service instance.

   ```javascript
   app_config = AppConfiguration.get_instance()
   app_config.init(region=AppConfiguration.REGION_US_SOUTH,
                  guid='GUID',
                  apikey='APIKEY')
   ```
   {: codeblock}

   where,
   - region: Region name where the service instance is created. For example, use `AppConfiguration.REGION_US_SOUTH` for Dallas.
   - guid: Instance Id of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - apikey: ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.

1. Initialize the feature with the following command:

   ```javascript
   app_config.set_collection_id(collection_id='collection_id') 
   ```
   {: codeblock}

   where,
   - collection_id: Id of the collection created in {{site.data.keyword.appconfig_short}} service instance.

1. *Optional*: You can work offline with local feature file and perform [feature operations](#ac-python-example).

   ```javascript
   app_config.fetch_features_from_file(feature_file='custom/userJson.json', # Add this field if liveFeatureUpdateEnabled false or get features when the device is offline during the first app load.
                                       live_feature_update_enabled=True) # This is for live update from server.
   ```
   {: codeblock}

   where,
   - liveFeatureUpdateEnabled: Set this value to `false` if the new feature values shouldn't be fetched from the server. Make sure to provide a proper JSON file in the `feature_file` path. By default, this value is `enabled`.
   - feature_file: Path to the JSON file which contains feature details and segment details.

### Examples for using feature related APIs
{: #ac-python-example}

Refer to the below examples for using the feature related APIs.

#### Get single feature
{: #ac-python-get-single-feature}

```javascript
feature = app_config.get_feature('feature_id')
```
{: codeblock}

#### Get all features
{: #ac-python-get-all-features}

```javascript
features_dictionary = app_config.get_features()
```
{: codeblock}

#### Feature evaluation
{: #ac-python-feature-evaluation}

```javascript
identity = {
    'city': 'Bangalore',
    'country': 'India'
}
feature_value = feature.get_current_value(identity_id='pvQr45', identity_attributes=identity)
```
{: codeblock}

#### Listen to the feature data changes
{: #ac-python-listen-feature-changes}

To listen to the data changes, add the following code in your application:

```javascript
def features_update(self):
    print('Get your Feature value NOW')

app_config.register_features_update_listener(features_update)
```
{: codeblock}

#### Fetch latest data
{: #ac-python-fetch-latest-data}

```javascript
app_config.fetch_feature_data()
```
{: codeblock}