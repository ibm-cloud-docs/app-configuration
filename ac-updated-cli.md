---

copyright:
  years: 2026
lastupdated: "2026-01-13"

keywords: app configuration api, cli, plugin

---

{{site.data.keyword.attribute-definition-list}}

# App Configuration CLI (Valid for versions 2.0.0 and above)
{: #app-configuration-updated-cli}

To view the CLI commands for deprecated versions 0.0.1 to 1.0.14, see [App Configuration CLI commands (Valid only for versions 0.0.1 - 1.0.14)](/docs/app-configuration?topic=app-configuration-app-configuration-cli).
{: note}

The {{site.data.keyword.cloud_notm}} command-line interface (CLI) provides extra capabilities for service offerings. {{site.data.keyword.cloud_notm}} CLI supports a plug-in framework to extend its capability. You can install the {{site.data.keyword.appconfig_short}} CLI plug-in from the {{site.data.keyword.cloud_notm}} plug-in repository. With the {{site.data.keyword.appconfig_short}} service CLI plug-in, you can easily manage {{site.data.keyword.appconfig_short}} service instances by using the CLI commands.
{: shortdesc}

To run {{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_short}} commands, use `ibmcloud app-configuration` or `ibmcloud ac`.
{: tip}


## Prerequisites
{: #ac-updated-version-prereqs}

* An {{site.data.keyword.cloud_notm}} account. If you do not have an account, click [here](https://cloud.ibm.com/) to create one.
* An instance of [{{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_short}}](https://cloud.ibm.com/catalog/services/app-configuration) service.
* [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
* Optionally, if you want to use private endpoint support that is provided by the {{site.data.keyword.cloud_notm}} platform, make sure that you enable[VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint&interface=ui).

## Installing {{site.data.keyword.appconfig_short}} CLI plug-in
{: #ac-updated-version-install-cli}

Install the {{site.data.keyword.appconfig_short}} CLI plug-in by running the following command from the IBM plug-in repo `{{site.data.keyword.cloud_notm}}`:

```sh
ibmcloud plugin install app-configuration
```
{: pre}

You're notified on the command-line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use the new commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}

### Output
{: #ac-updated-version-install-cli-output}

The command returns the following output:

```sh
Looking up 'app-configuration' from repository 'IBM Cloud'...
Plug-in 'app-configuration' found in repository 'IBM Cloud'
Attempting to download the binary file...
[==============================================================================================================================================] 100.00%
Installing binary...
OK
Plug-in 'app-configuration' was successfully installed into /Users/<username>/.bluemix/plugins/app-configuration. Use 'ibmcloud plugin show app-configuration' to show its details.
```
{: screen}

## Logging in to the CLI with a private endpoint
{: #ac-updated-version-ibmcloud-login-cli-private-endpoint}

For enhanced control and security over your data when using CLI, you have the option of using private routes to {{site.data.keyword.cloud_notm}} endpoints. First enable virtual routing and forwarding in your account, and then you can enable the use of {{site.data.keyword.cloud_notm}} private service endpoints. For more information about setting up your account to support the private connectivity option, see [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint).

Use the following command to log in to a private endpoint by using the CLI:

```sh
ibmcloud login -a private.cloud.ibm.com
```
{: pre}

## Globals
{: #app-configuration-globals}

The file-input flag is available for only create and update commands. The file-output flag is available for all commands.
{: note}

Ensure that the order of the flags is correct to achieve desired output.
{: note}

### Commands
{: #app-configuration-commands}

#### `ibmcloud app-configuration docs`
{: #app-configuration-cli-docs-command}

Opens the plug-in documentation in the web browser.

```sh
ibmcloud app-configuration docs
```

##### Example
{: #app-configuration-docs-examples}

```sh
ibmcloud app-configuration docs
```
{: pre}

### Options
{: #app-configuration-global-options}

`--region` (string)
:   The region where you provisioned your App Configuration instance. Available values: us-south, eu-gb, au-syd, us-east, eu-de, ca-tor, jp-tok, jp-osa, eu-es, br-sao, ca-mon.

`--output` (string)
:   Choose an output format - can be 'json', 'yaml', or 'table'. Defaults to 'table'.

`-j`, `--jmes-query` (string)
:   Provide a JMESPath query to customize output.

`--service-url` (string)
:   Provide the base endpoint URL for the API.

`-q`, `--quiet`
:   Suppresses verbose messages.

`-v`, `--version`
:   Prints the plug-in version.

#### Example
{: #app-configuration-global-options-example}

```sh
ibmcloud app-configuration
    --region=us-south \
    --output=json \
    --jmes-query="[:10]" \
    --service-url=<service url>
    --quiet
```
{: pre}

Note: This example only demonstrates the global options available to all sub-commands and is not a valid command itself.

## Config
{: #app-configuration-cli-config-command}

Global parameters can also be stored in persistent configuration so that they do not need to be manually specified each time the plug-in is invoked. Each parameter can be configured with the `config` command and its subcommands.

```sh
ibmcloud app-configuration config
```

guid refers to the instance ID of your App Configuration instance. You can set this option on a global level or on the command level.
{: note}

### `ibmcloud app-configuration config set`
{: #app-configuration-cli-config-set-command}

Set a new config value for a specific option. Each subcommand of the `set` command maps to a global option. Each subcommand accepts a single argument, the string representation of the value to store for the option.

```sh
ibmcloud app-configuration config set <option> <value>
```

#### Examples
{: #app-configuration-config-set-command-examples}

```sh
ibmcloud app-configuration config set service-url \
    'https://{region}.apprapp.cloud.ibm.com'
```
{: pre}

### `ibmcloud app-configuration config get`
{: #app-configuration-cli-config-get-command}

Print out the currently set value for a specific option. Each subcommand of the `get` command maps to a global option.

```sh
ibmcloud app-configuration config get <option>
```

#### Examples
{: #app-configuration-config-get-command-examples}

```sh
ibmcloud app-configuration config get service-url
```
{: pre}

### `ibmcloud app-configuration config unset`
{: #app-configuration-cli-config-unset-command}

Unset the currently set value for a specific option. Each subcommand of the `unset` command maps to a global option.

The subcommands available for this service are: `service-url`, .

```sh
ibmcloud app-configuration config unset <option>
```

#### Examples
{: #app-configuration-config-unset-command-examples}

```sh
ibmcloud app-configuration config unset service-url
```
{: pre}

### `ibmcloud app-configuration config list`
{: #app-configuration-cli-config-list-command}

List out all of the currently set config values.

```sh
ibmcloud app-configuration config list
```

#### Examples
{: #app-configuration-config-list-command-examples}

```sh
ibmcloud app-configuration config list
```
{: pre}

## Environments
{: #app-configuration-environments-cli}

Environments represent your application environments.

### `ibmcloud app-configuration environments`
{: #app-configuration-cli-environments-command}

List all the environments in the App Configuration service instance.
Note: If the `--all-pages` option is not set, the command will only retrieve a single page of the collection.

```sh
ibmcloud app-configuration environments --guid GUID [--expand=EXPAND] [--sort SORT] [--tags TAGS] [--include INCLUDE] [--limit LIMIT] [--offset OFFSET] [--search SEARCH]
```


#### Command options
{: #app-configuration-environments-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--expand` (bool)
:   If set to `true`, returns expanded view of the resource details.

`--sort` (string)
:   Sort the environment details based on the specified attribute. By default, items are sorted by name.

    Allowable values are: `created_time`, `updated_time`, `id`, `name`.

`--tags` (string)
:   Filter the resources to be returned based on the associated tags. Specify the parameter as a list of comma separated tags. Returns resources associated with any of the specified tags.

`--include` ([]string)
:   Include feature, property, snapshots details in the response.

    Allowable list items are: `features`, `properties`, `snapshots`. The maximum length is `20` items. The minimum length is `0` items.

`--limit` (int64)
:   The number of records to retrieve. By default, the list operation return the first 10 records. To retrieve different set of records, use `limit` with `offset` to page through the available records.

    The default value is `10`. The maximum value is `100`. The minimum value is `1`.

`--offset` (int64)
:   The number of records to skip. By specifying `offset`, you retrieve a subset of items that starts with the `offset` value. Use `offset` with `limit` to page through the available records.

    The default value is `0`. The minimum value is `0`.

`--search` (string)
:   Searches for the provided keyword and returns the appropriate row with that value. Here the search happens on the '[Name OR Tag]' of the entity.

`--all-pages` (bool)
:   Invoke multiple requests to display all pages of the collection for environments.

#### Example
{: #app-configuration-environments-examples}

```sh
ibmcloud app-configuration environments \
    --guid exampleString \
    --expand=true \
    --sort created_time \
    --tags 'version 1.1,pre-release' \
    --include features,properties,snapshots \
    --limit 10 \
    --offset 0 \
    --search 'test tag'
```
{: pre}

### `ibmcloud app-configuration environment-create`
{: #app-configuration-cli-environment-create-command}

Create an environment.

```sh
ibmcloud app-configuration environment-create --guid GUID --name NAME --environment-id ENVIRONMENT-ID [--description DESCRIPTION] [--tags TAGS] [--color-code COLOR-CODE]
```


#### Command options
{: #app-configuration-environment-create-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--name` (string)
:   Environment name. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only. Required.

    The maximum length is `256` characters.

`--environment-id` (string)
:   Environment id. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only. Required.

    The maximum length is `256` characters.

`--description` (string)
:   Environment description.

    The maximum length is `255` characters.

`--tags` (string)
:   Tags associated with the environment, allowed special characters are [_. ,-:].

    The value must match regular expression `/^[a-zA-Z0-9_\\. ,\\-]+(:[a-zA-Z0-9_\\. ,\\-]+)*$/`.

`--color-code` (string)
:   Color code to distinguish the environment. The Hex code for the color. For example `#FF0000` for `red`.

#### Example
{: #app-configuration-environment-create-examples}

```sh
ibmcloud app-configuration environment-create \
    --guid exampleString \
    --name 'Dev environment' \
    --environment-id dev-environment \
    --description 'Dev environment description' \
    --tags development \
    --color-code #FDD13A
```
{: pre}

### `ibmcloud app-configuration environment-update`
{: #app-configuration-cli-environment-update-command}

Update an environment.

```sh
ibmcloud app-configuration environment-update --guid GUID --environment-id ENVIRONMENT-ID [--name NAME] [--description DESCRIPTION] [--tags TAGS] [--color-code COLOR-CODE]
```


#### Command options
{: #app-configuration-environment-update-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--name` (string)
:   Environment name. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only.

    The maximum length is `256` characters.

`--description` (string)
:   Environment description.

    The maximum length is `255` characters.

`--tags` (string)
:   Tags associated with the environment, allowed special characters are [_. ,-:].

    The value must match regular expression `/^[a-zA-Z0-9_\\. ,\\-]+(:[a-zA-Z0-9_\\. ,\\-]+)*$/`.

`--color-code` (string)
:   Color code to distinguish the environment. The Hex code for the color. For example `#FF0000` for `red`.

#### Example
{: #app-configuration-environment-update-examples}

```sh
ibmcloud app-configuration environment-update \
    --guid exampleString \
    --environment-id environment_id \
    --name exampleString \
    --description exampleString \
    --tags exampleString \
    --color-code #FDD13A
```
{: pre}

### `ibmcloud app-configuration environment`
{: #app-configuration-cli-environment-command}

Retrieve the details of the environment.

```sh
ibmcloud app-configuration environment --guid GUID --environment-id ENVIRONMENT-ID [--expand=EXPAND] [--include INCLUDE]
```


#### Command options
{: #app-configuration-environment-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--expand` (bool)
:   If set to `true`, returns expanded view of the resource details.

`--include` ([]string)
:   Include feature, property, snapshots details in the response.

    Allowable list items are: `features`, `properties`, `snapshots`. The maximum length is `20` items. The minimum length is `0` items.

#### Example
{: #app-configuration-environment-examples}

```sh
ibmcloud app-configuration environment \
    --guid exampleString \
    --environment-id environment_id \
    --expand=true \
    --include features,properties,snapshots
```
{: pre}

### `ibmcloud app-configuration environment-delete`
{: #app-configuration-cli-environment-delete-command}

Delete an Environment.

```sh
ibmcloud app-configuration environment-delete --guid GUID --environment-id ENVIRONMENT-ID
```


#### Command options
{: #app-configuration-environment-delete-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

#### Example
{: #app-configuration-environment-delete-examples}

```sh
ibmcloud app-configuration environment-delete \
    --guid exampleString \
    --environment-id environment_id
```
{: pre}

Use command option `-f` or `--force` if you want to delete without the confirmation prompt.
{: note}

## Collections
{: #app-configuration-collections-cli}

Collections are a way to group feature flags and properties.

### `ibmcloud app-configuration collections`
{: #app-configuration-cli-collections-command}

List of all the collections in the App Configuration service instance.
Note: If the `--all-pages` option is not set, the command will only retrieve a single page of the collection.

```sh
ibmcloud app-configuration collections --guid GUID [--expand=EXPAND] [--sort SORT] [--tags TAGS] [--features FEATURES] [--properties PROPERTIES] [--include INCLUDE] [--limit LIMIT] [--offset OFFSET] [--search SEARCH]
```


#### Command options
{: #app-configuration-collections-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--expand` (bool)
:   If set to `true`, returns expanded view of the resource details.

`--sort` (string)
:   Sort the collection details based on the specified attribute. By default, items are sorted by name.

    Allowable values are: `created_time`, `updated_time`, `id`, `name`.

`--tags` (string)
:   Filter the resources to be returned based on the associated tags. Specify the parameter as a list of comma separated tags. Returns resources associated with any of the specified tags.

`--features` ([]string)
:   Filter collections by a list of comma separated features.

    The maximum length is `20` items. The minimum length is `0` items.

`--properties` ([]string)
:   Filter collections by a list of comma separated properties.

    The maximum length is `20` items. The minimum length is `0` items.

`--include` ([]string)
:   Include feature, property, snapshots details in the response.

    Allowable list items are: `features`, `properties`, `snapshots`. The maximum length is `20` items. The minimum length is `0` items.

`--limit` (int64)
:   The number of records to retrieve. By default, the list operation return the first 10 records. To retrieve different set of records, use `limit` with `offset` to page through the available records.

    The default value is `10`. The maximum value is `100`. The minimum value is `1`.

`--offset` (int64)
:   The number of records to skip. By specifying `offset`, you retrieve a subset of items that starts with the `offset` value. Use `offset` with `limit` to page through the available records.

    The default value is `0`. The minimum value is `0`.

`--search` (string)
:   Searches for the provided keyword and returns the appropriate row with that value. Here the search happens on the '[Name OR Tag]' of the entity.

`--all-pages` (bool)
:   Invoke multiple requests to display all pages of the collection for collections.

#### Example
{: #app-configuration-collections-examples}

```sh
ibmcloud app-configuration collections \
    --guid exampleString \
    --expand=true \
    --sort created_time \
    --tags 'version 1.1,pre-release' \
    --features my-feature-id,cycle-rentals \
    --properties my-property-id,email-property \
    --include features,properties,snapshots \
    --limit 10 \
    --offset 0 \
    --search 'test tag'
```
{: pre}

### `ibmcloud app-configuration collection-create`
{: #app-configuration-cli-collection-create-command}

Create a collection.

```sh
ibmcloud app-configuration collection-create --guid GUID --name NAME --collection-id COLLECTION-ID [--description DESCRIPTION] [--tags TAGS]
```


#### Command options
{: #app-configuration-collection-create-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--name` (string)
:   Collection name. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only. Required.

    The maximum length is `256` characters.

`--collection-id` (string)
:   Collection Id. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only. Required.

    The maximum length is `256` characters.

`--description` (string)
:   Collection description.

    The maximum length is `255` characters.

`--tags` (string)
:   Tags associated with the collection, allowed special characters are [_. ,-:].

    The value must match regular expression `/^[a-zA-Z0-9_\\. ,\\-]+(:[a-zA-Z0-9_\\. ,\\-]+)*$/`.

#### Example
{: #app-configuration-collection-create-examples}

```sh
ibmcloud app-configuration collection-create \
    --guid exampleString \
    --name 'Web App Collection' \
    --collection-id web-app-collection \
    --description 'Collection for Web application' \
    --tags 'version: 1.1, pre-release'
```
{: pre}

### `ibmcloud app-configuration collection-update`
{: #app-configuration-cli-collection-update-command}

Update the collection name, tags and description. Collection Id cannot be updated.

```sh
ibmcloud app-configuration collection-update --guid GUID --collection-id COLLECTION-ID [--name NAME] [--description DESCRIPTION] [--tags TAGS]
```


#### Command options
{: #app-configuration-collection-update-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--collection-id` (string)
:   Collection Id of the collection. Required.

`--name` (string)
:   Collection name. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only.

    The maximum length is `256` characters.

`--description` (string)
:   Description of the collection.

    The maximum length is `255` characters.

`--tags` (string)
:   Tags associated with the collection, allowed special characters are [_. ,-:].

    The value must match regular expression `/^[a-zA-Z0-9_\\. ,\\-]+(:[a-zA-Z0-9_\\. ,\\-]+)*$/`.

#### Example
{: #app-configuration-collection-update-examples}

```sh
ibmcloud app-configuration collection-update \
    --guid exampleString \
    --collection-id collection_id \
    --name exampleString \
    --description exampleString \
    --tags exampleString
```
{: pre}

### `ibmcloud app-configuration collection`
{: #app-configuration-cli-collection-command}

Retrieve the details of the collection.

```sh
ibmcloud app-configuration collection --guid GUID --collection-id COLLECTION-ID [--expand=EXPAND] [--include INCLUDE]
```


#### Command options
{: #app-configuration-collection-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--collection-id` (string)
:   Collection Id of the collection. Required.

`--expand` (bool)
:   If set to `true`, returns expanded view of the resource details.

`--include` ([]string)
:   Include feature, property, snapshots details in the response.

    Allowable list items are: `features`, `properties`, `snapshots`. The maximum length is `20` items. The minimum length is `0` items.

#### Example
{: #app-configuration-collection-examples}

```sh
ibmcloud app-configuration collection \
    --guid exampleString \
    --collection-id collection_id \
    --expand=true \
    --include features,properties,snapshots
```
{: pre}

### `ibmcloud app-configuration collection-delete`
{: #app-configuration-cli-collection-delete-command}

Delete the collection.

```sh
ibmcloud app-configuration collection-delete --guid GUID --collection-id COLLECTION-ID
```


#### Command options
{: #app-configuration-collection-delete-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--collection-id` (string)
:   Collection Id of the collection. Required.

#### Example
{: #app-configuration-collection-delete-examples}

```sh
ibmcloud app-configuration collection-delete \
    --guid exampleString \
    --collection-id collection_id
```
{: pre}

Use command option `-f` or `--force` if you want to delete without the confirmation prompt.
{: note}

## Features
{: #app-configuration-features-cli}

Create and manage different types of feature flags for your apps and services.


### `ibmcloud app-configuration features`
{: #app-configuration-cli-features-command}

List all the feature flags in the specified environment.
Note: If the `--all-pages` option is not set, the command will only retrieve a single page of the collection.

```sh
ibmcloud app-configuration features --guid GUID --environment-id ENVIRONMENT-ID [--expand=EXPAND] [--sort SORT] [--tags TAGS] [--collections COLLECTIONS] [--segments SEGMENTS] [--include INCLUDE] [--limit LIMIT] [--offset OFFSET] [--search SEARCH]
```


#### Command options
{: #app-configuration-features-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--expand` (bool)
:   If set to `true`, returns expanded view of the resource details.

`--sort` (string)
:   Sort the feature details based on the specified attribute. By default, items are sorted by name.

    Allowable values are: `created_time`, `updated_time`, `id`, `name`.

`--tags` (string)
:   Filter the resources to be returned based on the associated tags. Specify the parameter as a list of comma separated tags. Returns resources associated with any of the specified tags.

`--collections` ([]string)
:   Filter features by a list of comma separated collections.

    The maximum length is `20` items. The minimum length is `0` items.

`--segments` ([]string)
:   Filter features by a list of comma separated segments.

    The maximum length is `20` items. The minimum length is `0` items.

`--include` ([]string)
:   Include the associated collections or targeting rules or change request details in the response.

    Allowable list items are: `collections`, `rules`, `change_request`. The maximum length is `20` items. The minimum length is `0` items.

`--limit` (int64)
:   The number of records to retrieve. By default, the list operation return the first 10 records. To retrieve different set of records, use `limit` with `offset` to page through the available records.

    The default value is `10`. The maximum value is `100`. The minimum value is `1`.

`--offset` (int64)
:   The number of records to skip. By specifying `offset`, you retrieve a subset of items that starts with the `offset` value. Use `offset` with `limit` to page through the available records.

    The default value is `0`. The minimum value is `0`.

`--search` (string)
:   Searches for the provided keyword and returns the appropriate row with that value. Here the search happens on the '[Name OR Tag]' of the entity.

`--all-pages` (bool)
:   Invoke multiple requests to display all pages of the collection for features.

#### Example
{: #app-configuration-features-examples}

```sh
ibmcloud app-configuration features \
    --guid exampleString \
    --environment-id environment_id \
    --expand=true \
    --sort created_time \
    --tags 'version 1.1,pre-release' \
    --collections my-collection-id,ghzindiapvtltd \
    --segments my-segment-id,beta-users \
    --include collections,rules,change_request \
    --limit 10 \
    --offset 0 \
    --search 'test tag'
```
{: pre}

### `ibmcloud app-configuration feature-create`
{: #app-configuration-cli-feature-create-command}

Create a feature flag.

```sh
ibmcloud app-configuration feature-create --guid GUID --environment-id ENVIRONMENT-ID --name NAME --feature-id FEATURE-ID --type TYPE --enabled-value ENABLED-VALUE --disabled-value DISABLED-VALUE [--description DESCRIPTION] [--format FORMAT] [--enabled=ENABLED] [--rollout-percentage ROLLOUT-PERCENTAGE] [--tags TAGS] [--segment-rules SEGMENT-RULES] [--collections COLLECTIONS]
```

If enabled value is set to **"true"**, then the collection must be provided. Else, the collection is optional.
{: note}

#### Command options
{: #app-configuration-feature-create-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--name` (string)
:   Feature name. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only. Required.

    The maximum length is `256` characters.

`--feature-id` (string)
:   Feature id. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only. Required.

    The maximum length is `256` characters.

`--type` (string)
:   Type of the feature (BOOLEAN, STRING, NUMERIC). If `type` is `STRING`, then `format` attribute is required. Required.

    Allowable values are: `BOOLEAN`, `STRING`, `NUMERIC`.

`--enabled-value` (interface{})
:   Value of the feature when it is enabled. The value can be Boolean, Numeric, String - TEXT, String - JSON, String - YAML value as per the `type` and `format` attributes. Required.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--enabled-value=@path/to/file.json`.

`--disabled-value` (interface{})
:   Value of the feature when it is disabled. The value can be Boolean, Numeric, String - TEXT, String - JSON, String - YAML value as per the `type` and `format` attributes. Required.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--disabled-value=@path/to/file.json`.

`--description` (string)
:   Feature description.

    The maximum length is `255` characters.

`--format` (string)
:   Format of the feature (TEXT, JSON, YAML) and it is a required attribute when `type` is `STRING`. It is not required for `BOOLEAN` and `NUMERIC` types. This property is populated in the response body of `POST, PUT and GET` calls if the type `STRING` is used and not populated for `BOOLEAN` and `NUMERIC` types.

    Allowable values are: `TEXT`, `JSON`, `YAML`.

`--enabled` (bool)
:   The state of the feature flag.

`--rollout-percentage` (int64)
:   Rollout percentage associated with feature flag. Supported only for Lite and Enterprise plans.

    The default value is `100`. The maximum value is `100`. The minimum value is `0`.

`--tags` (string)
:   Tags associated with the feature, allowed special characters are [_. ,-:].

    The value must match regular expression `/^[a-zA-Z0-9_\\. ,\\-]+(:[a-zA-Z0-9_\\. ,\\-]+)*$/`.

`--segment-rules` ([`FeatureSegmentRule[]`](#cli-feature-segment-rule-example-schema))
:   Specify the targeting rules that is used to set different feature flag values for different segments.

    The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--segment-rules=@path/to/file.json`.

`--collections` ([`CollectionRef[]`](#cli-collection-ref-example-schema))
:   List of collection id representing the collections that are associated with the specified feature flag.

    The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--collections=@path/to/file.json`.

#### Example
{: #app-configuration-feature-create-examples}

```sh
ibmcloud app-configuration feature-create \
    --guid exampleString \
    --environment-id environment_id \
    --name 'Cycle Rentals' \
    --feature-id cycle-rentals \
    --type BOOLEAN \
    --enabled-value "true" \
    --disabled-value "false" \
    --description 'Feature flag to enable Cycle Rentals' \
    --format TEXT \
    --enabled=true \
    --rollout-percentage 100 \
    --tags 'version: 1.1, pre-release' \
    --segment-rules '[{"rules": [{"segments": ["betausers","premiumusers"]}], "value": "true", "order": 1, "rollout_percentage": 50}]' \
    --collections '[{"collection_id": "ghzinc"}]'
```
{: pre}

### `ibmcloud app-configuration feature-update`
{: #app-configuration-cli-feature-update-command}

Update a feature flag details.

```sh
ibmcloud app-configuration feature-update --guid GUID --environment-id ENVIRONMENT-ID --feature-id FEATURE-ID [--name NAME] [--description DESCRIPTION] [--enabled-value ENABLED-VALUE] [--disabled-value DISABLED-VALUE] [--enabled=ENABLED] [--rollout-percentage ROLLOUT-PERCENTAGE] [--tags TAGS] [--segment-rules SEGMENT-RULES] [--collections COLLECTIONS]
```
If enabled value is set to **"true"**, then the collection must be provided. Else, the collection is optional.
{: note}

#### Command options
{: #app-configuration-feature-update-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--feature-id` (string)
:   Feature Id. Required.

`--name` (string)
:   Feature name. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only.

    The maximum length is `256` characters.

`--description` (string)
:   Feature description.

    The maximum length is `255` characters.

`--enabled-value` (interface{})
:   Value of the feature when it is enabled. The value can be Boolean, Numeric, String - TEXT, String - JSON, String - YAML value as per the `type` and `format` attributes.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--enabled-value=@path/to/file.json`.

`--disabled-value` (interface{})
:   Value of the feature when it is disabled. The value can be Boolean, Numeric, String - TEXT, String - JSON, String - YAML value as per the `type` and `format` attributes.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--disabled-value=@path/to/file.json`.

`--enabled` (bool)
:   The state of the feature flag.

`--rollout-percentage` (int64)
:   Rollout percentage associated with feature flag. Supported only for Lite and Enterprise plans.

    The default value is `100`. The maximum value is `100`. The minimum value is `0`.

`--tags` (string)
:   Tags associated with the feature, allowed special characters are [_. ,-:].

    The value must match regular expression `/^[a-zA-Z0-9_\\. ,\\-]+(:[a-zA-Z0-9_\\. ,\\-]+)*$/`.

`--segment-rules` ([`FeatureSegmentRule[]`](#cli-feature-segment-rule-example-schema))
:   Specify the targeting rules that is used to set different property values for different segments.

    The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--segment-rules=@path/to/file.json`.

`--collections` ([`CollectionUpdateRef[]`](#cli-collection-update-ref-example-schema))
:   List of collection id representing the collections that are associated with the specified property.

    The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--collections=@path/to/file.json`.

#### Example
{: #app-configuration-feature-update-examples}

```sh
ibmcloud app-configuration feature-update \
    --guid exampleString \
    --environment-id environment_id \
    --feature-id feature_id \
    --name 'Cycle Rentals' \
    --description 'Feature flags to enable Cycle Rentals' \
    --enabled-value "true" \
    --disabled-value "false" \
    --enabled=true \
    --rollout-percentage 100 \
    --tags 'version: 1.1, yet-to-release' \
    --segment-rules '[{"rules": [{"segments": ["betausers","premiumusers"]}], "value": "true", "order": 1, "rollout_percentage": 90}]' \
    --collections '[{"collection_id": "ghzinc", "deleted": true}]'
```
{: pre}

### `ibmcloud app-configuration feature-values-update`
{: #app-configuration-cli-feature-values-update-command}

Update the feature values. This method can be executed only by the `writer` role. This method allows the update of feature name, feature enabled_value, feature disabled_value, tags, description and feature segment rules, however this method does not allow toggling the feature flag and assigning feature to a collection.

```sh
ibmcloud app-configuration feature-values-update --guid GUID --environment-id ENVIRONMENT-ID --feature-id FEATURE-ID [--name NAME] [--description DESCRIPTION] [--tags TAGS] [--enabled-value ENABLED-VALUE] [--disabled-value DISABLED-VALUE] [--rollout-percentage ROLLOUT-PERCENTAGE] [--segment-rules SEGMENT-RULES]
```


#### Command options
{: #app-configuration-feature-values-update-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--feature-id` (string)
:   Feature Id. Required.

`--name` (string)
:   Feature name. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only.

    The maximum length is `256` characters.

`--description` (string)
:   Feature description.

    The maximum length is `255` characters.

`--tags` (string)
:   Tags associated with the feature, allowed special characters are [_. ,-:].

    The value must match regular expression `/^[a-zA-Z0-9_\\. ,\\-]+(:[a-zA-Z0-9_\\. ,\\-]+)*$/`.

`--enabled-value` (interface{})
:   Value of the feature when it is enabled. The value can be Boolean, Numeric, String - TEXT, String - JSON, String - YAML value as per the `type` and `format` attributes.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--enabled-value=@path/to/file.json`.

`--disabled-value` (interface{})
:   Value of the feature when it is disabled. The value can be Boolean, Numeric, String - TEXT, String - JSON, String - YAML value as per the `type` and `format` attributes.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--disabled-value=@path/to/file.json`.

`--rollout-percentage` (int64)
:   Rollout percentage associated with feature flag. Supported only for Lite and Enterprise plans.

    The default value is `100`. The maximum value is `100`. The minimum value is `0`.

`--segment-rules` ([`FeatureSegmentRule[]`](#cli-feature-segment-rule-example-schema))
:   Specify the targeting rules that is used to set different property values for different segments.

    The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--segment-rules=@path/to/file.json`.

#### Example
{: #app-configuration-feature-values-update-examples}

```sh
ibmcloud app-configuration feature-values-update \
    --guid exampleString \
    --environment-id environment_id \
    --feature-id feature_id \
    --name 'Cycle Rentals' \
    --description 'Feature flags to enable Cycle Rentals' \
    --tags 'version: 1.1, yet-to-release' \
    --enabled-value "true" \
    --disabled-value "false" \
    --rollout-percentage 100 \
    --segment-rules '[{"rules": [{"segments": ["betausers","premiumusers"]}], "value": "true", "order": 1, "rollout_percentage": 100}]'
```
{: pre}

### `ibmcloud app-configuration feature`
{: #app-configuration-cli-feature-command}

Retrieve details of a feature.

```sh
ibmcloud app-configuration feature --guid GUID --environment-id ENVIRONMENT-ID --feature-id FEATURE-ID [--include INCLUDE]
```


#### Command options
{: #app-configuration-feature-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--feature-id` (string)
:   Feature Id. Required.

`--include` ([]string)
:   Include the associated collections or targeting rules or change request details in the response.

    Allowable list items are: `collections`, `rules`, `change_request`. The maximum length is `20` items. The minimum length is `0` items.

#### Example
{: #app-configuration-feature-examples}

```sh
ibmcloud app-configuration feature \
    --guid exampleString \
    --environment-id environment_id \
    --feature-id feature_id \
    --include collections,rules,change_request
```
{: pre}

### `ibmcloud app-configuration feature-delete`
{: #app-configuration-cli-feature-delete-command}

Delete a feature flag.

```sh
ibmcloud app-configuration feature-delete --guid GUID --environment-id ENVIRONMENT-ID --feature-id FEATURE-ID
```


#### Command options
{: #app-configuration-feature-delete-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--feature-id` (string)
:   Feature Id. Required.

#### Example
{: #app-configuration-feature-delete-examples}

```sh
ibmcloud app-configuration feature-delete \
    --guid exampleString \
    --environment-id environment_id \
    --feature-id feature_id
```
{: pre}

Use command option `-f` or `--force` if you want to delete without the confirmation prompt.
{: note}

### `ibmcloud app-configuration feature-toggle`
{: #app-configuration-cli-feature-toggle-command}

Toggle a feature.

```sh
ibmcloud app-configuration feature-toggle --guid GUID --environment-id ENVIRONMENT-ID --feature-id FEATURE-ID --enabled=ENABLED
```


#### Command options
{: #app-configuration-feature-toggle-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--feature-id` (string)
:   Feature Id. Required.

`--enabled` (bool)
:   The state of the feature flag. Required.

#### Example
{: #app-configuration-feature-toggle-examples}

```sh
ibmcloud app-configuration feature-toggle \
    --guid exampleString \
    --environment-id environment_id \
    --feature-id feature_id \
    --enabled=true
```
{: pre}

## Properties
{: #app-configuration-properties-cli}

Create and manage different types of properties for your apps and services.

### `ibmcloud app-configuration properties`
{: #app-configuration-cli-properties-command}

List all the properties in the specified environment.
Note: If the `--all-pages` option is not set, the command will only retrieve a single page of the collection.

```sh
ibmcloud app-configuration properties --guid GUID --environment-id ENVIRONMENT-ID [--expand=EXPAND] [--sort SORT] [--tags TAGS] [--collections COLLECTIONS] [--segments SEGMENTS] [--include INCLUDE] [--limit LIMIT] [--offset OFFSET] [--search SEARCH]
```


#### Command options
{: #app-configuration-properties-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--expand` (bool)
:   If set to `true`, returns expanded view of the resource details.

`--sort` (string)
:   Sort the property details based on the specified attribute. By default, items are sorted by name.

    Allowable values are: `created_time`, `updated_time`, `id`, `name`.

`--tags` (string)
:   Filter the resources to be returned based on the associated tags. Specify the parameter as a list of comma separated tags. Returns resources associated with any of the specified tags.

`--collections` ([]string)
:   Filter properties by a list of comma separated collections.

    The maximum length is `20` items. The minimum length is `0` items.

`--segments` ([]string)
:   Filter properties by a list of comma separated segments.

    The maximum length is `20` items. The minimum length is `0` items.

`--include` ([]string)
:   Include the associated collections or targeting rules details in the response.

    Allowable list items are: `collections`, `rules`. The maximum length is `20` items. The minimum length is `0` items.

`--limit` (int64)
:   The number of records to retrieve. By default, the list operation return the first 10 records. To retrieve different set of records, use `limit` with `offset` to page through the available records.

    The default value is `10`. The maximum value is `100`. The minimum value is `1`.

`--offset` (int64)
:   The number of records to skip. By specifying `offset`, you retrieve a subset of items that starts with the `offset` value. Use `offset` with `limit` to page through the available records.

    The default value is `0`. The minimum value is `0`.

`--search` (string)
:   Searches for the provided keyword and returns the appropriate row with that value. Here the search happens on the '[Name OR Tag]' of the entity.

`--all-pages` (bool)
:   Invoke multiple requests to display all pages of the collection for properties.

#### Example
{: #app-configuration-properties-examples}

```sh
ibmcloud app-configuration properties \
    --guid exampleString \
    --environment-id environment_id \
    --expand=true \
    --sort created_time \
    --tags 'version 1.1,pre-release' \
    --collections my-collection-id,ghzindiapvtltd \
    --segments my-segment-id,beta-users \
    --include collections,rules \
    --limit 10 \
    --offset 0 \
    --search 'test tag'
```
{: pre}

### `ibmcloud app-configuration property-create`
{: #app-configuration-cli-property-create-command}

Create a Property.

```sh
ibmcloud app-configuration property-create --guid GUID --environment-id ENVIRONMENT-ID --name NAME --property-id PROPERTY-ID --type TYPE --value VALUE [--description DESCRIPTION] [--format FORMAT] [--tags TAGS] [--segment-rules SEGMENT-RULES] [--collections COLLECTIONS]
```


#### Command options
{: #app-configuration-property-create-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--name` (string)
:   Property name. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only. Required.

    The maximum length is `256` characters.

`--property-id` (string)
:   Property id. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only. Required.

    The maximum length is `256` characters.

`--type` (string)
:   Type of the property (BOOLEAN, STRING, NUMERIC, SECRETREF). If `type` is `STRING`, then `format` attribute is required. Required.

    Allowable values are: `BOOLEAN`, `STRING`, `NUMERIC`, `SECRETREF`. To see example usage of the different types, see [App Configuration API](https://cloud.ibm.com/apidocs/app-configuration#create-property-request).

`--value` (interface{})
:   Value of the Property. The value can be Boolean, Numeric, SecretRef, String - TEXT, String - JSON, String - YAML as per the `type` and `format` attributes. Required.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--value=@path/to/file.json`.

`--description` (string)
:   Property description.

    The maximum length is `255` characters.

`--format` (string)
:   Format of the property (TEXT, JSON, YAML) and it is a required attribute when `type` is `STRING`. It is not required for `BOOLEAN`, `NUMERIC` or `SECRETREF` types. This attribute is populated in the response body of `POST, PUT and GET` calls if the type `STRING` is used and not populated for `BOOLEAN`, `NUMERIC` and `SECRETREF` types.

    Allowable values are: `TEXT`, `JSON`, `YAML`.

`--tags` (string)
:   Tags associated with the property, allowed special characters are [_. ,-:].

    The value must match regular expression `/^[a-zA-Z0-9_\\. ,\\-]+(:[a-zA-Z0-9_\\. ,\\-]+)*$/`.

`--segment-rules` ([`SegmentRule[]`](#cli-segment-rule-example-schema))
:   Specify the targeting rules that is used to set different property values for different segments.

    The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--segment-rules=@path/to/file.json`.

`--collections` ([`CollectionRef[]`](#cli-collection-ref-example-schema))
:   List of collection id representing the collections that are associated with the specified property.

    The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--collections=@path/to/file.json`.

#### Example
{: #app-configuration-property-create-examples}

```sh
ibmcloud app-configuration property-create \
    --guid exampleString \
    --environment-id environment_id \
    --name 'Email property' \
    --property-id email-property \
    --type BOOLEAN \
    --value "true" \
    --description 'Property for email' \
    --format TEXT \
    --tags 'version: 1.1, pre-release' \
    --segment-rules '[{"rules": [{"segments": ["betausers","premiumusers"]}], "value": "true", "order": 1}]' \
    --collections '[{"collection_id": "ghzinc"}]'
```
{: pre}

### `ibmcloud app-configuration property-update`
{: #app-configuration-cli-property-update-command}

Update a Property.

```sh
ibmcloud app-configuration property-update --guid GUID --environment-id ENVIRONMENT-ID --property-id PROPERTY-ID [--name NAME] [--description DESCRIPTION] [--value VALUE] [--tags TAGS] [--segment-rules SEGMENT-RULES] [--collections COLLECTIONS]
```


#### Command options
{: #app-configuration-property-update-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--property-id` (string)
:   Property Id. Required.

`--name` (string)
:   Property name. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only.

    The maximum length is `256` characters.

`--description` (string)
:   Property description.

    The maximum length is `255` characters.

`--value` (interface{})
:   Value of the Property. The value can be Boolean, Numeric, SecretRef, String - TEXT, String - JSON, String - YAML as per the `type` and `format` attributes. To see example usage of the different types, see [App Configuration API](https://cloud.ibm.com/apidocs/app-configuration#update-property-request).

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--value=@path/to/file.json`.

`--tags` (string)
:   Tags associated with the property, allowed special characters are [_. ,-:].

    The value must match regular expression `/^[a-zA-Z0-9_\\. ,\\-]+(:[a-zA-Z0-9_\\. ,\\-]+)*$/`.

`--segment-rules` ([`SegmentRule[]`](#cli-segment-rule-example-schema))
:   Specify the targeting rules that is used to set different property values for different segments.

    The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--segment-rules=@path/to/file.json`.

`--collections` ([`CollectionUpdateRef[]`](#cli-collection-update-ref-example-schema))
:   List of collection id representing the collections that are associated with the specified property.

    The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--collections=@path/to/file.json`.

#### Example
{: #app-configuration-property-update-examples}

```sh
ibmcloud app-configuration property-update \
    --guid exampleString \
    --environment-id environment_id \
    --property-id property_id \
    --name 'Email property' \
    --description 'Property for email' \
    --value "true" \
    --tags 'version: 1.1, pre-release' \
    --segment-rules '[{"rules": [{"segments": ["betausers","premiumusers"]}], "value": "true", "order": 1}]' \
    --collections '[{"collection_id": "ghzinc", "deleted": true}]'
```
{: pre}

### `ibmcloud app-configuration property-values-update`
{: #app-configuration-cli-property-values-update-command}

Update the property values. This method can be executed by the `writer` role. Property value and targeting rules can be updated, however this method does not allow assigning property to a collection.

```sh
ibmcloud app-configuration property-values-update --guid GUID --environment-id ENVIRONMENT-ID --property-id PROPERTY-ID [--name NAME] [--description DESCRIPTION] [--tags TAGS] [--value VALUE] [--segment-rules SEGMENT-RULES]
```


#### Command options
{: #app-configuration-property-values-update-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--property-id` (string)
:   Property Id. Required.

`--name` (string)
:   Property name. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only.

    The maximum length is `256` characters.

`--description` (string)
:   Property description.

    The maximum length is `255` characters.

`--tags` (string)
:   Tags associated with the property, allowed special characters are [_. ,-:].

    The value must match regular expression `/^[a-zA-Z0-9_\\. ,\\-]+(:[a-zA-Z0-9_\\. ,\\-]+)*$/`.

`--value` (interface{})
:   Value of the Property. The value can be Boolean, Numeric, SecretRef, String - TEXT, String - JSON, String - YAML as per the `type` and `format` attributes.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--value=@path/to/file.json`.

    To see example usage of the different types, see [App Configuration API](https://cloud.ibm.com/apidocs/app-configuration#update-property-values-request).

`--segment-rules` ([`SegmentRule[]`](#cli-segment-rule-example-schema))
:   Specify the targeting rules that is used to set different property values for different segments.

    The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--segment-rules=@path/to/file.json`.

#### Example
{: #app-configuration-property-values-update-examples}

```sh
ibmcloud app-configuration property-values-update \
    --guid exampleString \
    --environment-id environment_id \
    --property-id property_id \
    --name 'Email property' \
    --description 'Property for email' \
    --tags 'version: 1.1, pre-release' \
    --value "true" \
    --segment-rules '[{"rules": [{"segments": ["betausers","premiumusers"]}], "value": "true", "order": 1}]'
```
{: pre}

### `ibmcloud app-configuration property`
{: #app-configuration-cli-property-command}

Retrieve details of a property.

```sh
ibmcloud app-configuration property --guid GUID --environment-id ENVIRONMENT-ID --property-id PROPERTY-ID [--include INCLUDE]
```


#### Command options
{: #app-configuration-property-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--property-id` (string)
:   Property Id. Required.

`--include` ([]string)
:   Include the associated collections or targeting rules details in the response.

    Allowable list items are: `collections`, `rules`. The maximum length is `20` items. The minimum length is `0` items.

#### Example
{: #app-configuration-property-examples}

```sh
ibmcloud app-configuration property \
    --guid exampleString \
    --environment-id environment_id \
    --property-id property_id \
    --include collections,rules
```
{: pre}

### `ibmcloud app-configuration property-delete`
{: #app-configuration-cli-property-delete-command}

Delete a Property.

```sh
ibmcloud app-configuration property-delete --guid GUID --environment-id ENVIRONMENT-ID --property-id PROPERTY-ID
```


#### Command options
{: #app-configuration-property-delete-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--property-id` (string)
:   Property Id. Required.

#### Example
{: #app-configuration-property-delete-examples}

```sh
ibmcloud app-configuration property-delete \
    --guid exampleString \
    --environment-id environment_id \
    --property-id property_id
```
{: pre}

Use command option `-f` or `--force` if you want to delete without the confirmation prompt.
{: note}

## Segments
{: #app-configuration-segments-cli}

Segments define a group of users or resources based on rules. Feature flags or Properties can target segments to deliver variants of a feature or property.

### `ibmcloud app-configuration segments`
{: #app-configuration-cli-segments-command}

List all the segments.
Note: If the `--all-pages` option is not set, the command will only retrieve a single page of the collection.

```sh
ibmcloud app-configuration segments --guid GUID [--expand=EXPAND] [--sort SORT] [--tags TAGS] [--include INCLUDE] [--limit LIMIT] [--offset OFFSET] [--search SEARCH]
```


#### Command options
{: #app-configuration-segments-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--expand` (bool)
:   If set to `true`, returns expanded view of the resource details.

`--sort` (string)
:   Sort the segment details based on the specified attribute. By default, items are sorted by name.

    Allowable values are: `created_time`, `updated_time`, `id`, `name`.

`--tags` (string)
:   Filter the resources to be returned based on the associated tags. Specify the parameter as a list of comma separated tags. Returns resources associated with any of the specified tags.

`--include` (string)
:   Segment details to include the associated rules in the response.

    Allowable values are: `rules`.

`--limit` (int64)
:   The number of records to retrieve. By default, the list operation return the first 10 records. To retrieve different set of records, use `limit` with `offset` to page through the available records.

    The default value is `10`. The maximum value is `100`. The minimum value is `1`.

`--offset` (int64)
:   The number of records to skip. By specifying `offset`, you retrieve a subset of items that starts with the `offset` value. Use `offset` with `limit` to page through the available records.

    The default value is `0`. The minimum value is `0`.

`--search` (string)
:   Searches for the provided keyword and returns the appropriate row with that value. Here the search happens on the '[Name OR Tag]' of the entity.

`--all-pages` (bool)
:   Invoke multiple requests to display all pages of the collection for segments.

#### Example
{: #app-configuration-segments-examples}

```sh
ibmcloud app-configuration segments \
    --guid exampleString \
    --expand=true \
    --sort created_time \
    --tags 'version 1.1,pre-release' \
    --include rules \
    --limit 10 \
    --offset 0 \
    --search 'test tag'
```
{: pre}

### `ibmcloud app-configuration segment-create`
{: #app-configuration-cli-segment-create-command}

Create a segment.

```sh
ibmcloud app-configuration segment-create --guid GUID --name NAME --segment-id SEGMENT-ID --rules RULES [--description DESCRIPTION] [--tags TAGS]
```


#### Command options
{: #app-configuration-segment-create-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--name` (string)
:   Segment name. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only. Required.

    The maximum length is `256` characters.

`--segment-id` (string)
:   Segment id. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only. Required.

    The maximum length is `256` characters.

`--rules` ([`Rule[]`](#cli-rule-example-schema))
:   List of rules that determine if the entity belongs to the segment during feature / property evaluation. An entity is identified by an unique identifier and the attributes that it defines. Any feature flag and property value evaluation is performed in the context of an entity when it is targeted to segments. Required.

    The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--rules=@path/to/file.json`.

`--description` (string)
:   Segment description.

    The maximum length is `255` characters.

`--tags` (string)
:   Tags associated with the segments, allowed special characters are [_. ,-:].

    The value must match regular expression `/^[a-zA-Z0-9_\\. ,\\-]+(:[a-zA-Z0-9_\\. ,\\-]+)*$/`.

#### Example
{: #app-configuration-segment-create-examples}

```sh
ibmcloud app-configuration segment-create \
    --guid exampleString \
    --name 'Beta Users' \
    --segment-id beta-users \
    --rules '[{"attribute_name": "email", "operator": "endsWith", "values": ["@in.mnc.com","@us.mnc.com"]}]' \
    --description 'Segment containing the beta users' \
    --tags 'version: 1.1, stage'
```
{: pre}

### `ibmcloud app-configuration segment-update`
{: #app-configuration-cli-segment-update-command}

Update the segment properties.

```sh
ibmcloud app-configuration segment-update --guid GUID --segment-id SEGMENT-ID [--name NAME] [--description DESCRIPTION] [--tags TAGS] [--rules RULES]
```


#### Command options
{: #app-configuration-segment-update-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--segment-id` (string)
:   Segment Id. Required.

`--name` (string)
:   Segment name. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only.

    The maximum length is `256` characters.

`--description` (string)
:   Segment description.

    The maximum length is `255` characters.

`--tags` (string)
:   Tags associated with segments, allowed special characters are [_. ,-:].

    The value must match regular expression `/^[a-zA-Z0-9_\\. ,\\-]+(:[a-zA-Z0-9_\\. ,\\-]+)*$/`.

`--rules` ([`Rule[]`](#cli-rule-example-schema))
:   List of rules that determine if the entity belongs to the segment during feature / property evaluation. An entity is identified by an unique identifier and the attributes that it defines. Any feature flag and property value evaluation is performed in the context of an entity when it is targeted to segments.

    The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--rules=@path/to/file.json`.

#### Example
{: #app-configuration-segment-update-examples}

```sh
ibmcloud app-configuration segment-update \
    --guid exampleString \
    --segment-id segment_id \
    --name exampleString \
    --description exampleString \
    --tags exampleString \
    --rules '[{"attribute_name": "exampleString", "operator": "is", "values": ["exampleString","anotherTestString"]}]'
```
{: pre}

### `ibmcloud app-configuration segment`
{: #app-configuration-cli-segment-command}

Retrieve details of a segment.

```sh
ibmcloud app-configuration segment --guid GUID --segment-id SEGMENT-ID [--include INCLUDE]
```


#### Command options
{: #app-configuration-segment-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--segment-id` (string)
:   Segment Id. Required.

`--include` ([]string)
:   Include feature and property details in the response.

    Allowable list items are: `features`, `properties`. The maximum length is `20` items. The minimum length is `0` items.

#### Example
{: #app-configuration-segment-examples}

```sh
ibmcloud app-configuration segment \
    --guid exampleString \
    --segment-id segment_id \
    --include features,properties
```
{: pre}

### `ibmcloud app-configuration segment-delete`
{: #app-configuration-cli-segment-delete-command}

Delete a segment.

```sh
ibmcloud app-configuration segment-delete --guid GUID --segment-id SEGMENT-ID
```


#### Command options
{: #app-configuration-segment-delete-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--segment-id` (string)
:   Segment Id. Required.

#### Example
{: #app-configuration-segment-delete-examples}

```sh
ibmcloud app-configuration segment-delete \
    --guid exampleString \
    --segment-id segment_id
```
{: pre}

Use command option `-f` or `--force` if you want to delete without the confirmation prompt.
{: note}

## Snapshots
{: #app-configuration-snapshots-cli}

Snapshots are a way to capture the current configuration of your app or environment and sync the modified config into a Git repo.

### `ibmcloud app-configuration gitconfigs`
{: #app-configuration-cli-gitconfigs-command}

List all the Git configs.
Note: If the `--all-pages` option is not set, the command will only retrieve a single page of the collection.

```sh
ibmcloud app-configuration gitconfigs --guid GUID [--sort SORT] [--collection-id COLLECTION-ID] [--environment-id ENVIRONMENT-ID] [--limit LIMIT] [--offset OFFSET] [--search SEARCH]
```


#### Command options
{: #app-configuration-gitconfigs-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--sort` (string)
:   Sort the git configurations details based on the specified attribute. By default, items are sorted by name.

    Allowable values are: `created_time`, `updated_time`, `id`, `name`.

`--collection-id` (string)
:   Filters the response based on the specified collection_id.

`--environment-id` (string)
:   Filters the response based on the specified environment_id.

`--limit` (int64)
:   The number of records to retrieve. By default, the list operation return the first 10 records. To retrieve different set of records, use `limit` with `offset` to page through the available records.

    The default value is `10`. The maximum value is `100`. The minimum value is `1`.

`--offset` (int64)
:   The number of records to skip. By specifying `offset`, you retrieve a subset of items that starts with the `offset` value. Use `offset` with `limit` to page through the available records.

    The default value is `0`. The minimum value is `0`.

`--search` (string)
:   Searches for the provided keyword and returns the appropriate row with that value. Here the search happens on the '[Name]' of the entity.

`--all-pages` (bool)
:   Invoke multiple requests to display all pages of the collection for gitconfigs.

#### Example
{: #app-configuration-gitconfigs-examples}

```sh
ibmcloud app-configuration gitconfigs \
    --guid exampleString \
    --sort created_time \
    --collection-id collection_id \
    --environment-id environment_id \
    --limit 10 \
    --offset 0 \
    --search search_string
```
{: pre}

### `ibmcloud app-configuration gitconfig-create`
{: #app-configuration-cli-gitconfig-create-command}

Create a Git config.

```sh
ibmcloud app-configuration gitconfig-create --guid GUID --git-config-name GIT-CONFIG-NAME --git-config-id GIT-CONFIG-ID --collection-id COLLECTION-ID --environment-id ENVIRONMENT-ID --git-url GIT-URL --git-branch GIT-BRANCH --git-file-path GIT-FILE-PATH --git-token GIT-TOKEN
```


#### Command options
{: #app-configuration-gitconfig-create-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--git-config-name` (string)
:   Git config name. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only. Required.

    The maximum length is `100` characters.

`--git-config-id` (string)
:   Git config id. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only. Required.

    The maximum length is `30` characters.

`--collection-id` (string)
:   Collection Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--git-url` (string)
:   Git url which will be used to connect to the github account. The url must be formed in this format, https://api.github.com/repos/{owner}/{repo_name} for the personal git account. If you are using the organization account then url must be in this format https://github.{organization_name}.com/api/v3/repos/{owner}/{repo_name} . Note do not provide /(slash) in the beginning or at the end of the url. Required.

`--git-branch` (string)
:   Branch name to which you need to write or update the configuration. Just provide the branch name, do not provide any /(slashes) in the beginning or at the end of the branch name. Note make sure branch exists in your repository. Required.

`--git-file-path` (string)
:   Git file path, this is a path where your configuration file will be written. The path must contain the file name with `json` extension. We only create or update `json` extension file. Note do not provide any /(slashes) in the beginning or at the end of the file path. Required.

`--git-token` (string)
:   Git token, this needs to be provided with enough permission to write and update the file. Required.

#### Example
{: #app-configuration-gitconfig-create-examples}

```sh
ibmcloud app-configuration gitconfig-create \
    --guid exampleString \
    --git-config-name boot-strap-configuration \
    --git-config-id boot-strap-configuration \
    --collection-id web-app-collection \
    --environment-id dev \
    --git-url https://github.<company-name>.com/api/v3/repos/jhondoe-owner/my-test-repo \
    --git-branch main \
    --git-file-path code/development/README.json \
    --git-token 61a792eahhGHji223jijb55a6cfdd4d5cde4c8a67esjjhjhHVH
```
{: pre}

### `ibmcloud app-configuration gitconfig-update`
{: #app-configuration-cli-gitconfig-update-command}

Update the gitconfig properties.

```sh
ibmcloud app-configuration gitconfig-update --guid GUID --git-config-id GIT-CONFIG-ID [--git-config-name GIT-CONFIG-NAME] [--collection-id COLLECTION-ID] [--environment-id ENVIRONMENT-ID] [--git-url GIT-URL] [--git-branch GIT-BRANCH] [--git-file-path GIT-FILE-PATH] [--git-token GIT-TOKEN]
```


#### Command options
{: #app-configuration-gitconfig-update-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--git-config-id` (string)
:   Git Config Id. Required.

`--git-config-name` (string)
:   Git config name. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only.

    The maximum length is `100` characters.

`--collection-id` (string)
:   Collection Id.

`--environment-id` (string)
:   Environment Id.

`--git-url` (string)
:   Git url which will be used to connect to the github account. The url must be formed in this format, https://api.github.com/repos/{owner}/{repo_name} for the personal git account. If you are using the organization account then url must be in this format https://github.{organization_name}.com/api/v3/repos/{owner}/{repo_name} . Note do not provide /(slash) in the beginning or at the end of the url.

`--git-branch` (string)
:   Branch name to which you need to write or update the configuration. Just provide the branch name, do not provide any /(slashes) in the beginning or at the end of the branch name. Note make sure branch exists in your repository.

`--git-file-path` (string)
:   Git file path, this is a path where your configuration file will be written. The path must contain the file name with `json` extension. We only create or update `json` extension file. Note do not provide any /(slashes) in the beginning or at the end of the file path.

`--git-token` (string)
:   Git token, this needs to be provided with enough permission to write and update the file.

#### Example
{: #app-configuration-gitconfig-update-examples}

```sh
ibmcloud app-configuration gitconfig-update \
    --guid exampleString \
    --git-config-id git_config_id \
    --git-config-name exampleString \
    --collection-id exampleString \
    --environment-id exampleString \
    --git-url exampleString \
    --git-branch exampleString \
    --git-file-path exampleString \
    --git-token exampleString
```
{: pre}

### `ibmcloud app-configuration gitconfig`
{: #app-configuration-cli-gitconfig-command}

Retrieve details of a gitconfig.

```sh
ibmcloud app-configuration gitconfig --guid GUID --git-config-id GIT-CONFIG-ID
```


#### Command options
{: #app-configuration-gitconfig-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--git-config-id` (string)
:   Git Config Id. Required.

#### Example
{: #app-configuration-gitconfig-examples}

```sh
ibmcloud app-configuration gitconfig \
    --guid exampleString \
    --git-config-id git_config_id
```
{: pre}

### `ibmcloud app-configuration gitconfig-delete`
{: #app-configuration-cli-gitconfig-delete-command}

Delete a gitconfig.

```sh
ibmcloud app-configuration gitconfig-delete --guid GUID --git-config-id GIT-CONFIG-ID
```


#### Command options
{: #app-configuration-gitconfig-delete-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--git-config-id` (string)
:   Git Config Id. Required.

#### Example
{: #app-configuration-gitconfig-delete-examples}

```sh
ibmcloud app-configuration gitconfig-delete \
    --guid exampleString \
    --git-config-id git_config_id
```
{: pre}

Use command option `-f` or `--force` if you want to delete without the confirmation prompt.
{: note}

### `ibmcloud app-configuration gitconfig-promote`
{: #app-configuration-cli-gitconfig-promote-command}

Promote configuration, this api will write or update your chosen configuration to the GitHub based on the git url, file path and branch data. In simple words this api will create or updates the bootstrap json file.

```sh
ibmcloud app-configuration gitconfig-promote --guid GUID --git-config-id GIT-CONFIG-ID
```


#### Command options
{: #app-configuration-gitconfig-promote-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--git-config-id` (string)
:   Git Config Id. Required.

#### Example
{: #app-configuration-gitconfig-promote-examples}

```sh
ibmcloud app-configuration gitconfig-promote \
    --guid exampleString \
    --git-config-id git_config_id
```
{: pre}

### `ibmcloud app-configuration gitconfig-restore`
{: #app-configuration-cli-gitconfig-restore-command}

Restore configuration, this api will write or update your chosen configuration from the GitHub to App configuration instance. The api will read the contents in the json file that was created using promote API and recreate or updates the App configuration instance with the file contents like properties, features and segments.

```sh
ibmcloud app-configuration gitconfig-restore --guid GUID --git-config-id GIT-CONFIG-ID
```


#### Command options
{: #app-configuration-gitconfig-restore-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--git-config-id` (string)
:   Git Config Id. Required.

#### Example
{: #app-configuration-gitconfig-restore-examples}

```sh
ibmcloud app-configuration gitconfig-restore \
    --guid exampleString \
    --git-config-id git_config_id
```
{: pre}

## Integrations
{: #app-configuration-integrations-cli}

Integrations represent list of other IBM Cloud services that are connected to your App Configuration instance.

### `ibmcloud app-configuration integrations`
{: #app-configuration-cli-integrations-command}

List all the integrations.
Note: If the `--all-pages` option is not set, the command will only retrieve a single page of the collection.

```sh
ibmcloud app-configuration integrations --guid GUID [--expand=EXPAND] [--limit LIMIT] [--offset OFFSET]
```


#### Command options
{: #app-configuration-integrations-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--expand` (bool)
:   If set to `true`, returns expanded view of the resource details.

`--limit` (int64)
:   The number of records to retrieve. By default, the list operation return the first 10 records. To retrieve different set of records, use `limit` with `offset` to page through the available records.

    The default value is `10`. The maximum value is `100`. The minimum value is `1`.

`--offset` (int64)
:   The number of records to skip. By specifying `offset`, you retrieve a subset of items that starts with the `offset` value. Use `offset` with `limit` to page through the available records.

    The default value is `0`. The minimum value is `0`.

`--all-pages` (bool)
:   Invoke multiple requests to display all pages of the collection for integrations.

#### Example
{: #app-configuration-integrations-examples}

```sh
ibmcloud app-configuration integrations \
    --guid exampleString \
    --expand=true \
    --limit 10 \
    --offset 0
```
{: pre}

### `ibmcloud app-configuration integration-create`
{: #app-configuration-cli-integration-create-command}

Create an integration with App Configuration service instance.

```sh
ibmcloud app-configuration integration-create --guid GUID --integration-id INTEGRATION-ID --integration-type INTEGRATION-TYPE [--metadata METADATA | --metadata-event-notifications-instance-crn METADATA-EVENT-NOTIFICATIONS-INSTANCE-CRN --metadata-event-notifications-endpoint METADATA-EVENT-NOTIFICATIONS-ENDPOINT --metadata-event-notifications-source-name METADATA-EVENT-NOTIFICATIONS-SOURCE-NAME --metadata-event-notifications-source-description METADATA-EVENT-NOTIFICATIONS-SOURCE-DESCRIPTION --metadata-kms-instance-crn METADATA-KMS-INSTANCE-CRN --metadata-kms-endpoint METADATA-KMS-ENDPOINT --metadata-root-key-id METADATA-ROOT-KEY-ID]
```


#### Command options
{: #app-configuration-integration-create-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--integration-id` (string)
:   Integration id. Allowed special characters are dot ( . ), hyphen( - ), underscore ( _ ) only. Required.

`--integration-type` (string)
:   Integration type. Required.

    Allowable values are: `KMS`, `EVENT_NOTIFICATIONS`.

`--metadata` ([`CreateIntegrationMetadata`](#cli-create-integration-metadata-example-schema))
:   This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--metadata=@path/to/file.json`.

`--metadata-event-notifications-instance-crn` (string)
:   The CRN of the Event Notifications service instance. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

`--metadata-event-notifications-endpoint` (string)
:   The URL endpoint of the Event Notifications service instance. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

`--metadata-event-notifications-source-name` (string)
:   Source name. This name will be shown in your Event Notification instance sources page. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

`--metadata-event-notifications-source-description` (string)
:   Source description. This description will be shown in your Event Notification instance sources page under above source name. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

`--metadata-kms-instance-crn` (string)
:   The CRN of the Key Protect or HPCS service instance. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

`--metadata-kms-endpoint` (string)
:   The URL endpoint of Key Protect or HPCS instance. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

`--metadata-root-key-id` (string)
:   The rootkey id of Key Protect or HPCS instance. This option provides a value for a sub-field of the JSON option 'metadata'. It is mutually exclusive with that option.

#### Examples
{: #app-configuration-integration-create-examples}

```sh
ibmcloud app-configuration integration-create \
    --guid exampleString \
    --integration-id lckkhp34t \
    --integration-type EVENT_NOTIFICATIONS \
    --metadata '{"event_notifications_instance_crn": "crn:v1:bluemix:public:event-notifications:eu-gb:a/4f631ea3b3204b2b878a295604994acf:0eb42def-21aa-4f0a-a975-0812ead6ceee::", "event_notifications_endpoint": "https://eu-gb.event-notifications.cloud.ibm.com", "event_notifications_source_name": "My App Config", "event_notifications_source_description": "All the events from App Configuration instance"}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud app-configuration integration-create \
    --guid exampleString \
    --integration-id lckkhp34t \
    --integration-type EVENT_NOTIFICATIONS \
    --metadata-event-notifications-instance-crn crn:v1:bluemix:public:event-notifications:eu-gb:a/4f631ea3b3204b2b878a295604994acf:0eb42def-21aa-4f0a-a975-0812ead6ceee:: \
    --metadata-event-notifications-endpoint https://eu-gb.event-notifications.cloud.ibm.com \
    --metadata-event-notifications-source-name exampleString \
    --metadata-event-notifications-source-description exampleString
```
{: pre}

### `ibmcloud app-configuration integration`
{: #app-configuration-cli-integration-command}

Retrieve the details of the integration.

```sh
ibmcloud app-configuration integration --guid GUID --integration-id INTEGRATION-ID
```


#### Command options
{: #app-configuration-integration-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--integration-id` (string)
:   Integration Id of the integration. Required.

#### Example
{: #app-configuration-integration-examples}

```sh
ibmcloud app-configuration integration \
    --guid exampleString \
    --integration-id integration_id
```
{: pre}

### `ibmcloud app-configuration integration-delete`
{: #app-configuration-cli-integration-delete-command}

Delete an integration.

```sh
ibmcloud app-configuration integration-delete --guid GUID --integration-id INTEGRATION-ID
```


#### Command options
{: #app-configuration-integration-delete-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--integration-id` (string)
:   Integration Id of the integration. Required.

#### Example
{: #app-configuration-integration-delete-examples}

```sh
ibmcloud app-configuration integration-delete \
    --guid exampleString \
    --integration-id integration_id
```
{: pre}

Use command option `-f` or `--force` if you want to delete without the confirmation prompt.
{: note}

## Origin Config
{: #app-configuration-origin-config-cli}

Use settings to add more configurations required by external applications to access App Configuration resources.

### `ibmcloud app-configuration originconfigs`
{: #app-configuration-cli-originconfigs-command}

List all the Origin Configs.

```sh
ibmcloud app-configuration originconfigs --guid GUID
```


#### Command options
{: #app-configuration-originconfigs-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

#### Example
{: #app-configuration-originconfigs-examples}

```sh
ibmcloud app-configuration originconfigs \
    --guid exampleString
```
{: pre}

### `ibmcloud app-configuration originconfigs-update`
{: #app-configuration-cli-originconfigs-update-command}

Update the Origin Configs.

```sh
ibmcloud app-configuration originconfigs-update --guid GUID --allowed-origins ALLOWED-ORIGINS
```


#### Command options
{: #app-configuration-originconfigs-update-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--allowed-origins` ([]string)
:   List of allowed origins. Specify the parameter as a list of comma separated origins. Required.

    The maximum length is `20` items. The minimum length is `0` items.

#### Example
{: #app-configuration-originconfigs-update-examples}

```sh
ibmcloud app-configuration originconfigs-update \
    --guid exampleString \
    --allowed-origins exampleString,anotherTestString
```
{: pre}

## Workflow Configs
{: #app-configuration-workflow-configs-cli}

Manage feature flags enablement by adding additional workflow with ServiceNow® integration with App Configuration.

### `ibmcloud app-configuration workflowconfig`
{: #app-configuration-cli-workflowconfig-command}

Get the environment specific workflow configs.

```sh
ibmcloud app-configuration workflowconfig --guid GUID --environment-id ENVIRONMENT-ID
```


#### Command options
{: #app-configuration-workflowconfig-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

#### Example
{: #app-configuration-workflowconfig-examples}

```sh
ibmcloud app-configuration workflowconfig \
    --guid exampleString \
    --environment-id environment_id
```
{: pre}

### `ibmcloud app-configuration workflowconfig-create`
{: #app-configuration-cli-workflowconfig-create-command}

Create a Workflow.

```sh
ibmcloud app-configuration workflowconfig-create --guid GUID --environment-id ENVIRONMENT-ID [--workflow-config WORKFLOW-CONFIG | --workflow-config-workflow-url WORKFLOW-CONFIG-WORKFLOW-URL --workflow-config-approval-group-name WORKFLOW-CONFIG-APPROVAL-GROUP-NAME --workflow-config-approval-expiration WORKFLOW-CONFIG-APPROVAL-EXPIRATION --workflow-config-workflow-credentials WORKFLOW-CONFIG-WORKFLOW-CREDENTIALS --workflow-config-enabled=WORKFLOW-CONFIG-ENABLED --workflow-config-service-crn WORKFLOW-CONFIG-SERVICE-CRN --workflow-config-workflow-type WORKFLOW-CONFIG-WORKFLOW-TYPE --workflow-config-sm-instance-crn WORKFLOW-CONFIG-SM-INSTANCE-CRN --workflow-config-secret-id WORKFLOW-CONFIG-SECRET-ID]
```


#### Command options
{: #app-configuration-workflowconfig-create-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--workflow-config` ([`CreateWorkflowConfig`](#cli-create-workflow-config-example-schema))
:   The request body to create a new workflow config. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--workflow-config=@path/to/file.json`.

`--workflow-config-workflow-url` (string)
:   Only service now url https://xxxxx.service-now.com allowed, xxxxx is the service now instance id. This option provides a value for a sub-field of the JSON option 'workflow-config'. It is mutually exclusive with that option.

    The maximum length is `200` characters.

`--workflow-config-approval-group-name` (string)
:   Group name of personals who can approve the Change Request on your ServiceNow. It must be first registered in your ServiceNow then it must be added here. This option provides a value for a sub-field of the JSON option 'workflow-config'. It is mutually exclusive with that option.

    The maximum length is `100` characters.

`--workflow-config-approval-expiration` (int64)
:   Integer number identifies as hours which helps in adding approval start and end time to the created Change Request. This option provides a value for a sub-field of the JSON option 'workflow-config'. It is mutually exclusive with that option.

    The maximum value is `999`. The minimum value is `1`.

`--workflow-config-workflow-credentials` ([`ExternalServiceNowCredentials`](#cli-external-service-now-credentials-example-schema))
:   The credentials of the External ServiceNow instance. This option provides a value for a sub-field of the JSON option 'workflow-config'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--workflow-config-workflow-credentials=@path/to/file.json`.

`--workflow-config-enabled` (bool)
:   This option enables the workflow configuration per environment. User must set it to true if they wish to create Change Request for flag state changes. This option provides a value for a sub-field of the JSON option 'workflow-config'. It is mutually exclusive with that option.

    The default value is `false`.

`--workflow-config-service-crn` (string)
:   Only service crn will be allowed. Example: `crn:v1:staging:staging:appservice:us-south::::`. This option provides a value for a sub-field of the JSON option 'workflow-config'. It is mutually exclusive with that option.

    The maximum length is `255` characters.

`--workflow-config-workflow-type` (string)
:   Allowed value is `SERVICENOW_IBM` case-sensitive. This option provides a value for a sub-field of the JSON option 'workflow-config'. It is mutually exclusive with that option.

`--workflow-config-sm-instance-crn` (string)
:   Only Secret Manager instance crn will be allowed. Example: `crn:v1:staging:public:secrets-manager:eu-gb:a/3268cfe9e25d411122f9a731a:0a23274-92d0a-4d42-b1fa-d15b4293cd::`. This option provides a value for a sub-field of the JSON option 'workflow-config'. It is mutually exclusive with that option.

    The maximum length is `255` characters.

`--workflow-config-secret-id` (string)
:   Provide the arbitary secret key id which holds the api key to interact with service now. This is required to perform action on ServiceNow like Create CR or Close CR. This option provides a value for a sub-field of the JSON option 'workflow-config'. It is mutually exclusive with that option.

    The maximum length is `100` characters.

#### Examples
{: #app-configuration-workflowconfig-create-examples}

```sh
ibmcloud app-configuration workflowconfig-create \
    --guid exampleString \
    --environment-id environment_id \
    --workflow-config '{"workflow_url": "https://xxxxx.service-now.com", "approval_group_name": "WorkflowCRApprovers", "approval_expiration": 10, "workflow_credentials": {"username": "user", "password": "pwd", "client_id": "client id value", "client_secret": "clientsecret"}, "enabled": true}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud app-configuration workflowconfig-create \
    --guid exampleString \
    --environment-id environment_id \
    --workflow-config-workflow-url exampleString \
    --workflow-config-approval-group-name exampleString \
    --workflow-config-approval-expiration 1 \
    --workflow-config-workflow-credentials externalServiceNowCredentials \
    --workflow-config-enabled=false
```
{: pre}

### `ibmcloud app-configuration workflowconfig-update`
{: #app-configuration-cli-workflowconfig-update-command}

Update a Workflow.

```sh
ibmcloud app-configuration workflowconfig-update --guid GUID --environment-id ENVIRONMENT-ID [--update-workflow-config UPDATE-WORKFLOW-CONFIG | --update-workflow-config-workflow-url UPDATE-WORKFLOW-CONFIG-WORKFLOW-URL --update-workflow-config-approval-group-name UPDATE-WORKFLOW-CONFIG-APPROVAL-GROUP-NAME --update-workflow-config-approval-expiration UPDATE-WORKFLOW-CONFIG-APPROVAL-EXPIRATION --update-workflow-config-workflow-credentials UPDATE-WORKFLOW-CONFIG-WORKFLOW-CREDENTIALS --update-workflow-config-enabled=UPDATE-WORKFLOW-CONFIG-ENABLED --update-workflow-config-service-crn UPDATE-WORKFLOW-CONFIG-SERVICE-CRN --update-workflow-config-sm-instance-crn UPDATE-WORKFLOW-CONFIG-SM-INSTANCE-CRN --update-workflow-config-secret-id UPDATE-WORKFLOW-CONFIG-SECRET-ID]
```


#### Command options
{: #app-configuration-workflowconfig-update-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

`--update-workflow-config` ([`UpdateWorkflowConfig`](#cli-update-workflow-config-example-schema))
:   The request body to update an existing workflow config. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--update-workflow-config=@path/to/file.json`.

`--update-workflow-config-workflow-url` (string)
:   ServiceNow instance URL. Only url https://xxxxx.service-now.com allowed, xxxxx is the service now instance id. This option provides a value for a sub-field of the JSON option 'update-workflow-config'. It is mutually exclusive with that option.

    The maximum length is `200` characters.

`--update-workflow-config-approval-group-name` (string)
:   Group name of personals who can approve the Change Request on your ServiceNow. It must be first registered in your ServiceNow then it must be added here. This option provides a value for a sub-field of the JSON option 'update-workflow-config'. It is mutually exclusive with that option.

    The maximum length is `100` characters.

`--update-workflow-config-approval-expiration` (int64)
:   Integer number identifies as hours which helps in adding approval start and end time to the created Change Request. This option provides a value for a sub-field of the JSON option 'update-workflow-config'. It is mutually exclusive with that option.

    The maximum value is `999`. The minimum value is `1`.

`--update-workflow-config-workflow-credentials` ([`ExternalServiceNowCredentials`](#cli-external-service-now-credentials-example-schema))
:   The credentials of the External ServiceNow instance. This option provides a value for a sub-field of the JSON option 'update-workflow-config'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--update-workflow-config-workflow-credentials=@path/to/file.json`.

`--update-workflow-config-enabled` (bool)
:   This option enables the workflow configuration per environment. User must set it to true if they wish to create Change Request for flag state changes. This option provides a value for a sub-field of the JSON option 'update-workflow-config'. It is mutually exclusive with that option.

    The default value is `false`.

`--update-workflow-config-service-crn` (string)
:   Only service crn will be allowed. Example: `crn:v1:staging:staging:appservice:us-south::::`. This option provides a value for a sub-field of the JSON option 'update-workflow-config'. It is mutually exclusive with that option.

    The maximum length is `255` characters.

`--update-workflow-config-sm-instance-crn` (string)
:   Only Secret Manager instance crn will be allowed. Example: `crn:v1:staging:public:secrets-manager:eu-gb:a/3268cfe9e25d411122f9a731a:0a23274-92d0a-4d42-b1fa-d15b4293cd::`. This option provides a value for a sub-field of the JSON option 'update-workflow-config'. It is mutually exclusive with that option.

    The maximum length is `255` characters.

`--update-workflow-config-secret-id` (string)
:   Provide the arbitary secret key id which holds the api key to interact with service now. This is required to perform action on ServiceNow like Create CR or Close CR. This option provides a value for a sub-field of the JSON option 'update-workflow-config'. It is mutually exclusive with that option.

    The maximum length is `100` characters.

#### Examples
{: #app-configuration-workflowconfig-update-examples}

```sh
ibmcloud app-configuration workflowconfig-update \
    --guid exampleString \
    --environment-id environment_id \
    --update-workflow-config '{"workflow_url": "https://xxxxx.service-now.com", "approval_group_name": "WorkflowCRApprovers", "approval_expiration": 5, "workflow_credentials": {"username": "user", "password": "updated password", "client_id": "client id value", "client_secret": "updated client secret"}, "enabled": true}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud app-configuration workflowconfig-update \
    --guid exampleString \
    --environment-id environment_id \
    --update-workflow-config-workflow-url exampleString \
    --update-workflow-config-approval-group-name exampleString \
    --update-workflow-config-approval-expiration 1 \
    --update-workflow-config-workflow-credentials externalServiceNowCredentials \
    --update-workflow-config-enabled=false
```
{: pre}

### `ibmcloud app-configuration workflowconfig-delete`
{: #app-configuration-cli-workflowconfig-delete-command}

Delete a Workflow config.

```sh
ibmcloud app-configuration workflowconfig-delete --guid GUID --environment-id ENVIRONMENT-ID
```


#### Command options
{: #app-configuration-workflowconfig-delete-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environment-id` (string)
:   Environment Id. Required.

#### Example
{: #app-configuration-workflowconfig-delete-examples}

```sh
ibmcloud app-configuration workflowconfig-delete \
    --guid exampleString \
    --environment-id environment_id
```
{: pre}

Use command option `-f` or `--force` if you want to delete without the confirmation prompt.
{: note}

## Config
{: #app-configuration-config-cli}

Export and Import configurations from and to App Configuration instance.

### `ibmcloud app-configuration instance-import`
{: #app-configuration-cli-instance-import-command}

Import configuration to the instance.

```sh
ibmcloud app-configuration instance-import --guid GUID [--environments ENVIRONMENTS] [--collections COLLECTIONS] [--segments SEGMENTS] [--clean CLEAN]
```


#### Command options
{: #app-configuration-instance-import-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--environments` ([`ImportEnvironmentSchema[]`](#cli-import-environment-schema-example-schema))
:   Array will contain features and properties per environment.

    The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--environments=@path/to/file.json`.

`--collections` ([`ImportCollectionSchema[]`](#cli-import-collection-schema-example-schema))
:   Array will contain collections details.

    The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--collections=@path/to/file.json`.

`--segments` ([`ImportSegmentSchema[]`](#cli-import-segment-schema-example-schema))
:   Array will contain segments details.

    The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--segments=@path/to/file.json`.

`--clean` (string)
:   Full instance import requires query parameter `clean=true` to perform wiping of the existing data.

#### Example
{: #app-configuration-instance-import-examples}

```sh
ibmcloud app-configuration instance-import \
    --guid exampleString \
    --environments '[{"name": "Dev", "environment_id": "dev", "description": "Environment created on instance creation", "tags": "exampleString", "color_code": "#FDD13A", "features": [{"name": "Cycle Rentals", "feature_id": "cycle-rentals", "description": "exampleString", "type": "NUMERIC", "format": "TEXT", "enabled_value": "1", "disabled_value": "2", "enabled": true, "rollout_percentage": 100, "tags": "exampleString", "segment_rules": [{"rules": [{"segments": ["exampleString","anotherTestString"]}], "value": "exampleString", "order": 38, "rollout_percentage": 100}], "collections": [{"collection_id": "web-app"}]}], "properties": [{"name": "Daily Discount", "property_id": "daily_discount", "description": "exampleString", "type": "NUMERIC", "format": "TEXT", "value": "100", "tags": "pre-release, v1.2", "segment_rules": [{"rules": [{"segments": ["exampleString","anotherTestString"]}], "value": "200", "order": 1}], "collections": [{"collection_id": "web-app"}]}]}]' \
    --collections '[{"collection_id": "web-app", "name": "web-app", "description": "web app collection", "tags": "v1"}]' \
    --segments '[{"name": "Testers", "segment_id": "khpwj68h", "description": "Testers", "tags": "test", "rules": [{"attribute_name": "email", "operator": "is", "values": ["john@bluecharge.com","alice@bluecharge.com"]}]}]' \
    --clean true
```
{: pre}

### `ibmcloud app-configuration instance-export`
{: #app-configuration-cli-instance-export-command}

Get the instance configuration.

```sh
ibmcloud app-configuration instance-export --guid GUID
```


#### Command options
{: #app-configuration-instance-export-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

#### Example
{: #app-configuration-instance-export-examples}

```sh
ibmcloud app-configuration instance-export \
    --guid exampleString
```
{: pre}

### `ibmcloud app-configuration gitconfig-promote-restore`
{: #app-configuration-cli-gitconfig-promote-restore-command}

This api will either promote or restore your chosen configuration from or to the GitHub based on the git url, file path and branch data.

```sh
ibmcloud app-configuration gitconfig-promote-restore --guid GUID --git-config-id GIT-CONFIG-ID --action ACTION
```


#### Command options
{: #app-configuration-gitconfig-promote-restore-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--git-config-id` (string)
:   Git Config Id. Required.

`--action` (string)
:   Promote configuration to Git or Restore configuration from Git. Required.

    Allowable values are: `promote`, `restore`.

#### Example
{: #app-configuration-gitconfig-promote-restore-examples}

```sh
ibmcloud app-configuration gitconfig-promote-restore \
    --guid exampleString \
    --git-config-id git_config_id \
    --action promote
```
{: pre}

### `ibmcloud app-configuration instance-config-status`
{: #app-configuration-cli-instance-config-status-command}

Get the status of instance configuration operation.

```sh
ibmcloud app-configuration instance-config-status --guid GUID --reference-id REFERENCE-ID --action ACTION
```


#### Command options
{: #app-configuration-instance-config-status-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--reference-id` (string)
:   AppConfiguration config status reference id. Required.

`--action` (string)
:   The type of config status that is to be fetched. Required.

    Allowable values are: `import`, `export`.

#### Example
{: #app-configuration-instance-config-status-examples}

```sh
ibmcloud app-configuration instance-config-status \
    --guid exampleString \
    --reference-id exampleString \
    --action import
```
{: pre}

## Configuration Aggregator
{: #app-configuration-configuration-aggregator-cli}

The IBM cloud service to monitor configuration data of IBM services associated to Account.

### `ibmcloud app-configuration configs`
{: #app-configuration-cli-configs-command}

This is a beta release-level API. Retrieve the list of resource configurations collected as part of Configuration Aggregator.
Note: If the `--all-pages` option is not set, the command will only retrieve a single page of the collection.

```sh
ibmcloud app-configuration configs --guid GUID [--config-type CONFIG-TYPE] [--service-name SERVICE-NAME] [--resource-group-id RESOURCE-GROUP-ID] [--location LOCATION] [--resource-crn RESOURCE-CRN] [--limit LIMIT] [--start START] [--sub-account SUB-ACCOUNT] [--access-tags ACCESS-TAGS] [--user-tags USER-TAGS] [--service-tags SERVICE-TAGS]
```


#### Command options
{: #app-configuration-configs-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--config-type` (string)
:   The type of resource configuration that is to be fetched.

    The maximum length is `1024` characters. The minimum length is `1` character. The value must match regular expression `/^[a-zA-Z0-9 ,\\-_]+$/`.

`--service-name` (string)
:   The service from which the resource  is to be fetched.

    The maximum length is `1024` characters. The minimum length is `1` character. The value must match regular expression `/^[a-zA-Z0-9 ,\\-_]+$/`.

`--resource-group-id` (string)
:   The resource group id of the service.

    The maximum length is `32` characters. The minimum length is `0` characters. The value must match regular expression `/^[a-zA-Z0-9-]*$/`.

`--location` (string)
:   The location of the service.

    The maximum length is `32` characters. The minimum length is `0` characters. The value must match regular expression `/^$|[a-z]-[a-z]/`.

`--resource-crn` (string)
:   The crn of the resource.

    The maximum length is `1000` characters. The minimum length is `1` character. The value must match regular expression `/^[a-zA-Z0-9.\\:\/-]+$/`.

`--limit` (int64)
:   The number of resources for which the configuration can be fetched.

`--start` (string)
:   The start string to fetch the resource.

    The maximum length is `1000` characters. The minimum length is `1` character. The value must match regular expression `/[a-zA-Z0-9]/`.

`--sub-account` (string)
:   Filter the resource configurations from the specified sub-account in an enterprise hierarchy.

    The maximum length is `1000` characters. The minimum length is `1` character. The value must match regular expression `/[a-zA-Z0-9]/`.

`--access-tags` (string)
:   Filter the resource configurations attached with the specified access tags.

    The maximum length is `1000` characters. The minimum length is `1` character. The value must match regular expression `/[a-z0-9]/`.

`--user-tags` (string)
:   Filter the resource configurations attached with the specified user tags.

    The maximum length is `1000` characters. The minimum length is `1` character. The value must match regular expression `/[a-zA0-9]/`.

`--service-tags` (string)
:   Filter the resource configurations attached with the specified service tags.

    The maximum length is `1000` characters. The minimum length is `1` character. The value must match regular expression `/[a-z0-9]/`.

`--all-pages` (bool)
:   Invoke multiple requests to display all pages of the collection for configs.

#### Example
{: #app-configuration-configs-examples}

```sh
ibmcloud app-configuration configs \
    --guid exampleString \
    --config-type exampleString \
    --service-name exampleString \
    --resource-group-id exampleString \
    --location exampleString \
    --resource-crn exampleString \
    --limit 10 \
    --start exampleString \
    --sub-account exampleString \
    --access-tags role:admin \
    --user-tags test \
    --service-tags test:tag
```
{: pre}

### `ibmcloud app-configuration config-settings-update`
{: #app-configuration-cli-config-settings-update-command}

This is a beta release-level API. Replace the settings for resource collection as part of the Configuration Aggregator feature.

```sh
ibmcloud app-configuration config-settings-update --guid GUID [--resource-collection-enabled=RESOURCE-COLLECTION-ENABLED] [--trusted-profile-id TRUSTED-PROFILE-ID] [--regions REGIONS] [--additional-scope ADDITIONAL-SCOPE]
```


#### Command options
{: #app-configuration-config-settings-update-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

`--resource-collection-enabled` (bool)
:   The field denoting if the resource collection is enabled.

`--trusted-profile-id` (string)
:   The trusted profile id that provides Reader access to the App Configuration instance to collect resource metadata.

    Length must be `44` characters. The value must match regular expression `/^[a-zA-Z0-9-]*$/`.

`--regions` ([]string)
:   The list of regions across which the resource collection is enabled.

    The list items must match regular expression `/^[a-zA-Z0-9-]*$/`. The maximum length is `10` items. The minimum length is `0` items.

`--additional-scope` ([`AdditionalScope[]`](#cli-additional-scope-example-schema))
:   The additional scope that enables resource collection for Enterprise acccounts.

    The maximum length is `10` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--additional-scope=@path/to/file.json`.

#### Example
{: #app-configuration-config-settings-update-examples}

```sh
ibmcloud app-configuration config-settings-update \
    --guid exampleString \
    --resource-collection-enabled=true \
    --trusted-profile-id Profile-1260aec2-f2fc-44e2-8697-2cc15a447560 \
    --regions all \
    --additional-scope '[{"type": "Enterprise", "enterprise_id": "2c99aed413954f93b7cf7ce9fda6de61", "profile_template": {"id": "ProfileTemplate-adb55769-ae22-4c60-aead-bd1f84f93c57", "trusted_profile_id": "Profile-39acf232-8969-4c32-9838-83eb60a037f7"}}]'
```
{: pre}

### `ibmcloud app-configuration config-settings`
{: #app-configuration-cli-config-settings-command}

This is a beta release-level API. Retrieve settings for resource collection in Configuration Aggregator.

```sh
ibmcloud app-configuration config-settings --guid GUID
```


#### Command options
{: #app-configuration-config-settings-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

#### Example
{: #app-configuration-config-settings-examples}

```sh
ibmcloud app-configuration config-settings \
    --guid exampleString
```
{: pre}

### `ibmcloud app-configuration config-resource-collection-status`
{: #app-configuration-cli-config-resource-collection-status-command}

This is a beta release-level API. Retrieve the status of the resource collection as part of Configuration Aggregator.

```sh
ibmcloud app-configuration config-resource-collection-status --guid GUID
```


#### Command options
{: #app-configuration-config-resource-collection-status-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

#### Example
{: #app-configuration-config-resource-collection-status-examples}

```sh
ibmcloud app-configuration config-resource-collection-status \
    --guid exampleString
```
{: pre}

### `ibmcloud app-configuration config-manual-reconcile`
{: #app-configuration-cli-config-manual-reconcile-command}

Manually trigger the recording of the Configuration items as part of Configuration Aggregator.

```sh
ibmcloud app-configuration config-manual-reconcile --guid GUID
```


#### Command options
{: #app-configuration-config-manual-reconcile-cli-options}

`--guid` (string)
:   AppConfiguration instance Id. Required.

#### Example
{: #app-configuration-config-manual-reconcile-examples}

```sh
ibmcloud app-configuration config-manual-reconcile \
    --guid exampleString
```
{: pre}

## Schema examples
{: #app-configuration-schema-examples}

The following schema examples represent the data that you need to specify for a command option. These examples model the data structure and include placeholder values for the expected value type. When you run a command, replace these values with the values that apply to your environment as appropriate.

### AdditionalScope[]
{: #cli-additional-scope-example-schema}

The following example shows the format of the AdditionalScope[] object.

```json

[ {
  "type" : "Enterprise",
  "enterprise_id" : "2c99aed413954f93b7cf7ce9fda6de61",
  "profile_template" : {
    "id" : "ProfileTemplate-adb55769-ae22-4c60-aead-bd1f84f93c57",
    "trusted_profile_id" : "Profile-39acf232-8969-4c32-9838-83eb60a037f7"
  }
} ]
```
{: codeblock}

### CollectionRef[]
{: #cli-collection-ref-example-schema}

The following example shows the format of the CollectionRef[] object.

```json

[ {
  "collection_id" : "ghzinc"
} ]
```
{: codeblock}

### CollectionUpdateRef[]
{: #cli-collection-update-ref-example-schema}

The following example shows the format of the CollectionUpdateRef[] object.

```json

[ {
  "collection_id" : "ghzinc",
  "deleted" : true
} ]
```
{: codeblock}

### CreateIntegrationMetadata
{: #cli-create-integration-metadata-example-schema}

The following example shows the format of the CreateIntegrationMetadata object.

```json

{
  "event_notifications_instance_crn" : "crn:v1:bluemix:public:event-notifications:eu-gb:a/4f631ea3b3204b2b878a295604994acf:0eb42def-21aa-4f0a-a975-0812ead6ceee::",
  "event_notifications_endpoint" : "https://eu-gb.event-notifications.cloud.ibm.com",
  "event_notifications_source_name" : "My App Config",
  "event_notifications_source_description" : "All the events from App Configuration instance"
}
```
{: codeblock}

### CreateWorkflowConfig
{: #cli-create-workflow-config-example-schema}

The following example shows the format of the CreateWorkflowConfig object.

```json

{
  "workflow_url" : "https://xxxxx.service-now.com",
  "approval_group_name" : "WorkflowCRApprovers",
  "approval_expiration" : 10,
  "workflow_credentials" : {
    "username" : "user",
    "password" : "pwd",
    "client_id" : "client id value",
    "client_secret" : "clientsecret"
  },
  "enabled" : true
}
```
{: codeblock}

### ExternalServiceNowCredentials
{: #cli-external-service-now-credentials-example-schema}

The following example shows the format of the ExternalServiceNowCredentials object.

```json

{
  "username" : "admin",
  "password" : "Jy*1**Ef**q",
  "client_id" : "f7b6378b57d08210f8bdd233afc7256d",
  "client_secret" : "!xKxxxWTx"
}
```
{: codeblock}

### FeatureSegmentRule[]
{: #cli-feature-segment-rule-example-schema}

The following example shows the format of the FeatureSegmentRule[] object.

```json

[ {
  "rules" : [ {
    "segments" : [ "betausers", "premiumusers" ]
  } ],
  "value" : "true",
  "order" : 1,
  "rollout_percentage" : 50
} ]
```
{: codeblock}

### ImportCollectionSchema[]
{: #cli-import-collection-schema-example-schema}

The following example shows the format of the ImportCollectionSchema[] object.

```json

[ {
  "collection_id" : "web-app",
  "name" : "web-app",
  "description" : "web app collection",
  "tags" : "v1"
} ]
```
{: codeblock}

### ImportEnvironmentSchema[]
{: #cli-import-environment-schema-example-schema}

The following example shows the format of the ImportEnvironmentSchema[] object.

```json

[ {
  "name" : "Dev",
  "environment_id" : "dev",
  "description" : "Environment created on instance creation",
  "tags" : "exampleString",
  "color_code" : "#FDD13A",
  "features" : [ {
    "name" : "Cycle Rentals",
    "feature_id" : "cycle-rentals",
    "description" : "exampleString",
    "type" : "NUMERIC",
    "format" : "TEXT",
    "enabled_value" : "1",
    "disabled_value" : "2",
    "enabled" : true,
    "rollout_percentage" : 100,
    "tags" : "exampleString",
    "segment_rules" : [ {
      "rules" : [ {
        "segments" : [ "exampleString", "anotherExampleString" ]
      } ],
      "value" : "exampleString",
      "order" : 38,
      "rollout_percentage" : 100
    } ],
    "collections" : [ {
      "collection_id" : "web-app"
    } ]
  } ],
  "properties" : [ {
    "name" : "Daily Discount",
    "property_id" : "daily_discount",
    "description" : "exampleString",
    "type" : "NUMERIC",
    "format" : "TEXT",
    "value" : "100",
    "tags" : "pre-release, v1.2",
    "segment_rules" : [ {
      "rules" : [ {
        "segments" : [ "exampleString", "anotherExampleString" ]
      } ],
      "value" : "200",
      "order" : 1
    } ],
    "collections" : [ {
      "collection_id" : "web-app"
    } ]
  } ]
} ]
```
{: codeblock}

### ImportSegmentSchema[]
{: #cli-import-segment-schema-example-schema}

The following example shows the format of the ImportSegmentSchema[] object.

```json

[ {
  "name" : "Testers",
  "segment_id" : "khpwj68h",
  "description" : "Testers",
  "tags" : "test",
  "rules" : [ {
    "attribute_name" : "email",
    "operator" : "is",
    "values" : [ "john@bluecharge.com", "alice@bluecharge.com" ]
  } ]
} ]
```
{: codeblock}

### Rule[]
{: #cli-rule-example-schema}

The following example shows the format of the Rule[] object.

```json

[ {
  "attribute_name" : "email",
  "operator" : "endsWith",
  "values" : [ "@in.mnc.com", "@us.mnc.com" ]
} ]
```
{: codeblock}

### SegmentRule[]
{: #cli-segment-rule-example-schema}

The following example shows the format of the SegmentRule[] object.

```json

[ {
  "rules" : [ {
    "segments" : [ "betausers", "premiumusers" ]
  } ],
  "value" : "true",
  "order" : 1
} ]
```
{: codeblock}

### UpdateWorkflowConfig
{: #cli-update-workflow-config-example-schema}

The following example shows the format of the UpdateWorkflowConfig object.

```json

{
  "workflow_url" : "https://xxxxx.service-now.com",
  "approval_group_name" : "WorkflowCRApprovers",
  "approval_expiration" : 5,
  "workflow_credentials" : {
    "username" : "user",
    "password" : "updated password",
    "client_id" : "client id value",
    "client_secret" : "updated client secret"
  },
  "enabled" : true
}
```
{: codeblock}


## Sample input file
{: #cli-input-sample}


The following example shows the process of creating an environment using an input file:

Input File:

```json
environment_id: "E1"
name: "TestingEnv"
```

Command Line:

```sh
ibmcloud app-configuration environment-create \
    --guid exampleString \
    --name 'Dev environment' \
    --description 'Dev environment description' \
    --tags development \
    --color-code #FDD13A\
    --file-input 'Path to input file'
```


