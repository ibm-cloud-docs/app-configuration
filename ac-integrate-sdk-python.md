---

copyright:
  years: 2020, 2022
lastupdated: "2022-05-12"

keywords: app-configuration, app configuration, integrate sdk, python sdk, python

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# App Configuration server SDK for Python
{: #ac-python}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Python application.
{: shortdesc}

## Integrating server SDK for Python
{: #ac-integrate-python}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Python application. You can evaluate the values of your feature flag or property by integrating the {{site.data.keyword.appconfig_short}} SDK.

1. Use either one of the following methods to install the SDK:

 Using `pip`

   ```sh
   pip install --upgrade ibm-appconfiguration-python-sdk
   ```
   {: codeblock}

 Using `easy_install`

   ```py
   easy_install --upgrade ibm-appconfiguration-python-sdk
   ```
   {: codeblock}

1. In your Python application code, include the SDK module with:

   ```py
   from ibm_appconfiguration import AppConfiguration, Feature, Property, ConfigurationType
   ```
   {: codeblock}

1. Initialize the sdk to connect with your {{site.data.keyword.appconfig_short}} service instance.

   ```py
   appconfig_client = AppConfiguration.get_instance()
   appconfig_client.init(region=AppConfiguration.REGION_US_SOUTH, guid='GUID', apikey='APIKEY')
   appconfig_client.set_context(collection_id='collection_id', environment_id='environment_id')
   ```
   {: codeblock}

   Where:
- region: Region name where the service instance is created. Use `AppConfiguration.REGION_US_SOUTH` for Dallas, `AppConfiguration.REGION_US_EAST` for Washington DC, `AppConfiguration.REGION_EU_GB` for London, and `AppConfiguration.REGION_AU_SYD` for Sydney.
- guid: GUID of the {{site.data.keyword.appconfig_short}} service. Obtain it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
- apikey: ApiKey of the {{site.data.keyword.appconfig_short}} service. Obtain it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
- collection_id: ID of the collection created in {{site.data.keyword.appconfig_short}} service instance.
- environment_id: ID of the environment created in App Configuration service instance.
  
   The **`init()`** and **`set_context()`** are the initialisation methods and should be invoked **only once** by using appconfig_client. The appconfig_client, when initialized, can be obtained across modules by using **`AppConfiguration.get_instance()`**. For more information, see [Fetching the appconfig_client across other modules](#fetching-the-appconfig_client-across-other-modules).
   {: important}

### Option to use a persistent cache for configuration
{: #ac-python-persistent-cache}

For your application and SDK to continue operations even during the unlikely scenario of an {{site.data.keyword.appconfig_short}} service downtime, across your application restarts, you can configure the SDK to work by using a persistent cache. The SDK uses the persistent cache to store the {{site.data.keyword.appconfig_short}} data that is available across your application restarts.

```python
# 1. default (without persistent cache)
appconfig_client.set_context(collection_id='collection_id', environment_id='environment_id')

# 2. optional (with persistent cache)
appconfig_client.set_context(collection_id='collection_id', environment_id='environment_id', options={
  'persistent_cache_dir': '/var/lib/docker/volumes/'
})
```
{: codeblock}

Where,

- persistent_cache_dir: Absolute path to a directory that has read and write permission for the user. The SDK creates a file - `appconfiguration.json` in the specified directory, and it is used as the persistent cache to store the {{site.data.keyword.appconfig_short}} service information.
  
When persistent cache is enabled, the SDK keeps the last known good configuration at the persistent cache. If the {{site.data.keyword.appconfig_short}} server is unreachable, the latest configurations at the persistent cache are loaded to the application to continue working.

### Offline options
{: #ac-python-offline}

The SDK is also designed to serve configurations, and perform feature flag and property evaluations without being connected to {{site.data.keyword.appconfig_short}} service.

```python
appconfig_client.set_context(collection_id='collection_id', environment_id='environment_id', options={
  'bootstrap_file': 'saflights/flights.json',
  'live_config_update_enabled': False
})
```
{: codeblock}

Where,

- bootstrap_file: Absolute path of the JSON file, which contains configuration details. Make sure to provide a proper JSON file. You can generate this file by using `ibmcloud ac config` command of the IBM Cloud App Configuration CLI.

- live_config_update_enabled: Live configuration update from the server. Set this value to `False` if the new configuration values must not be fetched from the server. By default, this value is set to True.

### Examples for using feature and property-related APIs
{: #ac-python-example}

Refer to the listed examples for using the feature and property-related APIs.

#### Get single feature
{: #ac-python-get-single-feature}

```py
feature = appconfig_client.get_feature('feature_id')
if (feature) {
    print('Feature Name : {0}'.format(feature.get_feature_name()));
    print('Feature Id : {0}'.format(feature.get_feature_id()));
    print('Feature Type : {0}'.format(feature.get_feature_data_type()));
    print('Feature is enabled : {0}'.format(feature.is_enabled()));
}
```
{: codeblock}

#### Get all features
{: #ac-python-get-all-features}

```py
features_dictionary = appconfig_client.get_features()
```
{: codeblock}

#### Feature evaluation
{: #ac-python-feature-evaluation}

You can use the feature.get_current_value(entity_id, entity_attributes) method to evaluate the value of the feature flag. Pass a unique entity_id as the parameter to perform the feature flag evaluation. If the feature flag is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a dictionary.

```py
entity_attributes = {
    'city': 'Bangalore',
    'country': 'India'
}
feature_value = feature.get_current_value(entity_id='entity_id', entity_attributes=entity_attributes)
```
{: codeblock}

#### Get single Property
{: #ac-python-get-single-property}

```py
property = appconfig_client.get_property('property_id')
if (property) {
    print('Property Name : {0}'.format(property.get_property_name()));
    print('Property Id : {0}'.format(property.get_property_id()));
    print('Property Type : {0}'.format(property.get_property_data_type()));
}
```
{: codeblock}

#### Get all Properties
{: #ac-python-get-all-properties}

```py
properties_dictionary = appconfig_client.get_properties()
```
{: codeblock}

#### Property evaluation
{: #ac-python-property-evaluation}

You can use the `property.get_current_value(entity_id, entity_attributes)` method to evaluate the value of the property.

Pass a unique `entity_id` as the parameter to perform the property evaluation. If the property is configured with segments in the {{site.data.keyword.appconfig_short}} service, you can set the attributes values as a dictionary.

```py
entity_attributes = {
    'city': 'Bangalore',
    'country': 'India'
}
property_value = property.get_current_value(entity_id='entity_id', entity_attributes=entity_attributes)
```
{: codeblock}

### Fetching the appconfig_client across other modules
{: #fetching-the-appconfig_client-across-other-modules}

When the SDK is initialized, the appconfig_client can be obtained across other modules as shown:

```python
# **other modules**

from ibm_appconfiguration import AppConfiguration

appconfig_client = AppConfiguration.get_instance()
feature = appconfig_client.get_feature('feature_id')
enabled = feature.is_enabled()
feature_value = feature.get_current_value(entity_id, entity_attributes)
```
{: codeblock}

## Supported data types
{: #ac-integrate-pyth-supported-data-types}

You can configure feature flags and properties with {{site.data.keyword.appconfig_short}} service, supporting the following data types: Boolean, Numeric, and String. The String data type can be of the format of a TEXT string, JSON, or YAML. The SDK processes each
format as shown in the table.

| **Feature or Property value**                                                                          | **Data type** | **Data format** | **Type of data returned by `GetCurrentValue()`** | **Example output**                                                                 |
| ------------------------------------------------------------------------------------------------------ | ------------- | --------------- | ----------------------------------------------------- | ---------------------------------------------------------------------------------- |
| `true`                                                                                                 | BOOLEAN       | Not applicable  | `bool`                                                | `true`                                                                             |
| `25`                                                                                                   | NUMERIC       | Not applicable  | `int`                                                 | `25`                                                                               |
| "a string text"                                                                                        | STRING        | TEXT            | `string`                                              | `a string text`                                                                    |
| `{"firefox": {`  \n `"name": "Firefox",`  \n  `"pref_url": "about:config"`  \n }} | STRING | JSON | `Dictionary or List of Dictionary` | `{'firefox': {'name': 'Firefox', 'pref_url': 'about:config'}}` |
| `men:`  \n   `- John Smith`   \n`- Bill Jones`\n `women:`  \n   `- Mary Smith`   \n`- Susan Williams` | STRING | YAML | `Dictionary` | `{'men': ['John Smith', 'Bill Jones'], 'women': ['Mary Smith', 'Susan Williams']}` |
{: caption="Table 1. Example outputs" caption-side="bottom"}

### Feature flag
{: #ac-integrate-pyth-feat-flag}

```py
  feature = appconfig_client.get_feature('json-feature')
  feature.get_feature_data_type() // STRING
  feature.get_feature_data_format() // JSON
  feature.get_current_value(entityId, entityAttributes) // returns single dictionary object or list of dictionary object

  // Example Below
  // input json :- [{"role": "developer", "description": "do coding"},{"role": "tester", "description": "do testing"}]
  // expected output :- "do coding"

  tar_val = feature.get_current_value(entityId, entityAttributes)
  expected_output = tar_val[0]['description']

  // input json :- {"role": "tester", "description": "do testing"}
  // expected output :- "tester"

  tar_val = feature.get_current_value(entityId, entityAttributes)
  expected_output = tar_val['role']

  feature = appconfig_client.getFeature('yaml-feature')
  feature.get_feature_data_type() // STRING
  feature.get_feature_data_format() // YAML
  feature.get_current_value(entityId, entityAttributes) // returns dictionary object

  // Example Below
  // input yaml string :- "---\nrole: tester\ndescription: do_testing"
  // expected output :- "do_testing"

  tar_val = feature.get_current_value(entityId, entityAttributes)
  expected_output = tar_val['description']
```
{: codeblock}


#### Property
{: #ac-integrate-pyth-prop}

```py
  property = appconfig_client.get_property('json-property')
  property.get_property_data_type() // STRING
  property.get_property_data_format() // JSON
  property.get_current_value(entityId, entityAttributes) // returns single dictionary object or list of dictionary object

  // Example Below
  // input json :- [{"role": "developer", "description": "do coding"},{"role": "tester", "description": "do testing"}]
  // expected output :- "do coding"

  tar_val = property.get_current_value(entityId, entityAttributes)
  expected_output = tar_val[0]['description']

  // input json :- {"role": "tester", "description": "do testing"}
  // expected output :- "tester"

  tar_val = property.get_current_value(entityId, entityAttributes)
  expected_output = tar_val['role']

  property = appconfig_client.get_property('yaml-property')
  property.get_property_data_type() // STRING
  property.get_property_data_format() // YAML
  property.get_current_value(entityId, entityAttributes) // returns dictionary object

  // Example Below
  // input yaml string :- "---\nrole: tester\ndescription: do_testing"
  // expected output :- "do_testing"

  tar_val = property.get_current_value(entityId, entityAttributes)
  expected_output = tar_val['description']
```
{: codeblock}

#### Set listener for the feature and property data changes
{: #ac-python-listen-feature-and-property-changes}

The SDK provides mechanism to notify you in real time when feature flags' or properties' configuration changes. You can subscribe to configuration changes by using the same appconfig_client.

```py
def configuration_update(self):
    print('Received updates on configurations')
    # **add your code**
    # To find the effect of any configuration changes, you can call the feature or property related methods

    # feature = appconfig_client.getFeature('feature_id')
    # new_value = feature.get_current_value(entity_id, entity_attributes)

appconfig_client.register_configuration_update_listener(configuration_update)

```
{: codeblock}

#### Fetch latest data
{: #ac-python-fetch-latest-data}

```py
appconfig_client.fetch_configurations()
```
{: codeblock}
