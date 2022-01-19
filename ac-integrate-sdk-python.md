---

copyright:
  years: 2020, 2021
lastupdated: "2022-01-19"

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
{: shortdesc}

## Integrating server SDK for Python
{: #ac-integrate-python}

{{site.data.keyword.appconfig_short}} service provides SDK to integrate with your Python application. You can evaluate the values of your feature flag or property by integrating the {{site.data.keyword.appconfig_short}} SDK.

1.Use either one of the following methods to install the SDK:

 Using `pip`

      ```sh
      pip install --upgrade ibm-appconfiguration-python-sdk
      ```
      {: codeblock}

 Using `easy_install`

      ```
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
   app_config = AppConfiguration.get_instance()
   app_config.init(region=AppConfiguration.REGION_US_SOUTH,
                  guid='GUID',
                  apikey='APIKEY')

   ## Initialize configurations
   app_config.set_context(collection_id='collection_id',
                       environment_id='environment_id')
   ```
   {: codeblock}

   where,
   - region: Region name where the service instance is created. Use `AppConfiguration.REGION_US_SOUTH` for Dallas, `AppConfiguration.REGION_US_EAST` for Washington DC, `AppConfiguration.REGION_EU_GB` for London, and `AppConfiguration.REGION_AU_SYD` for Sydney.
   - guid: GUID of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - apikey: ApiKey of the {{site.data.keyword.appconfig_short}} service. Get it from the service credentials section of the {{site.data.keyword.appconfig_short}} service dashboard.
   - collection_id: ID of the collection created in {{site.data.keyword.appconfig_short}} service instance.
   - environment_id: ID of the environment created in App Configuration service instance.

1. *Optional*: You can work [offline](/docs/app-configuration?topic=app-configuration-ac-offline) with local configuration file and perform [feature and property operations](#ac-python-example).

   ```py
   ## set the file or offline configurations
   app_config.set_context(collection_id='collection_id',
                        environment_id='environment_id',
                        configuration_file='custom/userJson.json',
                        live_config_update_enabled=True)
   ```
   {: codeblock}

   where,
   - configuration_file: Path to the JSON file, which contains configuration details.
   - live_config_update_enabled: Set this value to `false` if new configuration values are not to be fetched from the server. Make sure to provide a proper JSON file in the `configuration_file` path. By default, this value is `enabled`.


### Examples for using feature and property-related APIs
{: #ac-python-example}

Refer to the listed examples for using the feature and property-related APIs.

#### Get single feature
{: #ac-python-get-single-feature}

```py
feature = app_config.get_feature('feature_id')
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
features_dictionary = app_config.get_features()
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
property = app_config.get_property('property_id')
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
properties_dictionary = app_config.get_properties()
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

## Supported data types
{: #ac-integrate-pyth-supported-data-types}

You can configure feature flags and properties with {{site.data.keyword.appconfig_short}} service, supporting the  following data types: Boolean, Numeric, and String. The String data type can be of the format of a TEXT string, JSON, or YAML. The SDK processes each
format as shown in the table.

| **Feature or Property value**                                                                                      | **Data type** | **Data format** | **Type of data returned <br> by `GetCurrentValue()`** | **Example output**                                                   |
| ------------------------------------------------------------------------------------------------------------------ | ------------ | -------------- | ----------------------------------------------------- | -------------------------------------------------------------------- |
| `true`                                                                                                             | BOOLEAN      | not applicable | `bool`                                                | `true`                                                               |
| `25`                                                                                                               | NUMERIC      | not applicable | `int`                                             | `25`                                                                 |
| "a string text"                                                                                                    | STRING       | TEXT           | `string`                                              | `a string text`                                                      |
| <pre>{<br>  "firefox": {<br>    "name": "Firefox",<br>    "pref_url": "about:config"<br>  }<br>}</pre> | STRING       | JSON           | `Dictionary or List of Dictionary`                              | `{'firefox': {'name': 'Firefox', 'pref_url': 'about:config'}}` |
| <pre>men:<br>  - John Smith<br>  - Bill Jones<br>women:<br>  - Mary Smith<br>  - Susan Williams</pre>  | STRING       | YAML           | `Dictionary`                              | `{'men': ['John Smith', 'Bill Jones'], 'women': ['Mary Smith', 'Susan Williams']}` |

#### Feature flag

```py
  feature = client.get_feature('json-feature')
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

  feature = client.getFeature('yaml-feature')
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

  ```py
  property = client.get_property('json-property')
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

  property = client.get_property('yaml-property')
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

#### Listen to the feature and property data changes
{: #ac-python-listen-feature-changes}

To listen to the data changes, add the following code in your application:

```py
def configuration_update(self):
    print('Get your Feature/Property value now')

app_config.register_configuration_update_listener(configuration_update)

```
{: codeblock}

#### Fetch latest data
{: #ac-python-fetch-latest-data}

```py
app_config.fetch_configurations()
```
{: codeblock}
