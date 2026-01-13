---

copyright:
  years: 2021, 2023
lastupdated: "2023-10-04"

keywords: app configuration CLI, app configuration command line, app configuration terminal, app configuration shell

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# App Configuration CLI commands (Valid only for versions 0.0.1 - 1.0.14)
{: #app-configuration-cli}

The CLI commands listed here will be valid only for versions 0.0.1 - 1.0.14 which will be deprecated.
{: deprecated}

The {{site.data.keyword.cloud_notm}} command-line interface (CLI) provides extra capabilities for service offerings. {{site.data.keyword.cloud_notm}} CLI supports a plug-in framework to extend its capability. You can install the {{site.data.keyword.appconfig_short}} CLI plug-in from the {{site.data.keyword.cloud_notm}} plug-in repository. With the {{site.data.keyword.appconfig_short}} service CLI plug-in, you can easily manage {{site.data.keyword.appconfig_short}} service instances by using the CLI commands.
{: shortdesc}

To run {{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_short}} commands, use `ibmcloud app-configuration` or `ibmcloud ac`.
{: tip}

## Prerequisites
{: #ac-prereqs}

* An {{site.data.keyword.cloud_notm}} account. If you do not have an account, click [here](https://cloud.ibm.com/) to create one.
* An instance of [{{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_short}}](https://cloud.ibm.com/catalog/services/app-configuration) service.
* [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
* Optionally, if you want to use private endpoint support that is provided by the {{site.data.keyword.cloud_notm}} platform, make sure that you enable[VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint&interface=ui).

## Installing {{site.data.keyword.appconfig_short}} CLI plug-in
{: #ac-install-cli}

Install the {{site.data.keyword.appconfig_short}} CLI plug-in by running the following command from the IBM plug-in repo `{{site.data.keyword.cloud_notm}}`:

```sh
ibmcloud plugin install app-configuration
```
{: pre}

You're notified on the command-line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use the new commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}

### Output
{: #ac-install-cli-output}

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
{: #ac-ibmcloud-login-cli-private-endpoint}

For enhanced control and security over your data when using CLI, you have the option of using private routes to {{site.data.keyword.cloud_notm}} endpoints. First enable virtual routing and forwarding in your account, and then you can enable the use of {{site.data.keyword.cloud_notm}} private service endpoints. For more information about setting up your account to support the private connectivity option, see [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint).

Use the following command to log in to a private endpoint by using the CLI:

```sh
ibmcloud login -a private.cloud.ibm.com
```
{: pre}

## ibmcloud ac init
{: #ac-ibmcloud-ac-init}

Before initializing the CLI plug-in, make sure that you select the correct API endpoint, region, and account in your {{site.data.keyword.cloud_notm}} CLI.
{: note}

Initialize the cli plug-in by using the following command:

```sh
ibmcloud ac init --instance_id INSTANCE_ID
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-init-command}

`--instance_id INSTANCE_ID` (optional)
:  GUID of the App Configuration instance to use.

### Example
{: #ac-ibmcloud-ac-init-example}

Log in to {{site.data.keyword.cloud_notm}} CLI and initialize the CLI to {{site.data.keyword.appconfig_short}} service instance `App Configuration Instance 1`.

```sh
ibmcloud ac init
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-init-output}

The command returns the following output (Instance name followed by a space along with GUID):

```sh
Initializing IBM Cloud App Configuration Service plug-in...

Select a App Configuration instance:
1. App_Configuration_Instance_1 123
2. App_Configuration_Instance_2 456
Enter a number> 1
App Configuration instance selected is - App_Configuration_Instance_1 (GUID - 123)
```
{: screen}

## ibmcloud ac show
{: #ac-ibmcloud-ac-show}

To see the name and GUID of the instance that is being used, use this command.

```sh
ibmcloud ac show
```
{: pre}

### Example
{: #ac-ibmcloud-ac-show-example}

Prerequisite - Use the `ibmcloud ac init` command to select an instance first.
{: note}

```sh
ibmcloud ac show
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-show-output}

The command returns the following output:

```
App Configuration instance being used is - App_Configuration_Instance_1 (GUID - 123)
```
{: screen}

## ibmcloud ac environment list
{: #ac-ibmcloud-ac-environment-list}

You can list all environments, by using the command:

```sh
ibmcloud ac environment list [--expand EXPAND] [--sort SORT] [--tags TAGS] [--include INCLUDE] [--limit LIMIT] [--offset OFFSET]
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-environment-list-command-options}

`--limit LIMIT` (optional)
:  Used for pagination. The number of records to retrieve.

`--offset OFFSET` (optional)
:  Used for pagination. The number of records to skip.

`--tags TAGS` (optional)
:  Filter based on the tags.

`--sort SORT` (optional)
:  Sort the details based on the specified attribute.

`--expand EXPAND` (optional)
:  Expanded view of the item.

`--include INCLUDE` (optional)
:  Include feature and property details in the response.

### Example
{: #ac-ibmcloud-ac-environment-list-example}

To list all environments, run the following command:

```sh
ibmcloud ac environment list
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-environment-list-output}

The command returns the following output:

```sh
name               environment_id
Prod Environment   prodEnvironment
Dev environment    devEnvironment
```
{: screen}

## ibmcloud ac environment create
{: #ac-ibmcloud-ac-environment-create}

You can create an environment by using the command:

```sh
ibmcloud ac environment create {--file FILE-PATH | --name NAME [--environment_id ENVIRONMENT_ID] [--description DESCRIPTION] [--tags TAGS] [--color_code COLOR_CODE]}
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-environment-create-command}

`--name NAME`
:  Environment name. Required field - input either as a flag or from file.

`--environment_id ENVIRONMENT_ID` (optional)
:  Environment ID. If this value is not provided, the name will automatically become the ID. Optional field - input either as a flag or from file.

`--description DESCRIPTION` (optional)
:  Description of the environment. Optional field - input either as a flag or from file.

`--tags TAGS` (optional)
:  Tags associated with the environment. Optional field - input either as a flag or from file.

`--color_code COLOR_CODE` (optional)
:  Color code to distinguish the environment. The Hex code for the color. Optional field - input either as a flag or from file.

`--file FILE`
:  Input through the file. File format Supported - JSON

### Example
{: #ac-ibmcloud-ac-environment-create-example}

To create an environment with name `Production_Environment` using flags ([click here](#ac-fileinput) for using commands with `--file` flag), run the following command:

```sh
ibmcloud ac environment create --name Production_Environment --environment_id prodEnvironment --description sampleDesc --tags sampleTag --color_code "#FF0000"
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-environment-create-output}

The command returns the following output:

```sh
updated_time     2021-05-21T05:28:07.000Z
name             Production_Environment
environment_id   prodEnvironment
description      sampleDesc
tags             sampleTag
color_code       #FF0000
created_time     2021-05-21T05:28:07.000Z
```
{: screen}

## ibmcloud ac environment get
{: #ac-ibmcloud-ac-environment-get}

You can get an environment detail by using the command:

```sh
ibmcloud ac environment get --environment_id ENVIRONMENT_ID [--expand EXPAND] [--include INCLUDE]
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-environment-get-command}

`--environment_id ENVIRONMENT_ID`
:  Environment ID

`--expand EXPAND` (optional)
:  Expanded view of the item.

`--include INCLUDE` (optional)
:  Include feature and property details in the response.

### Example
{: #ac-ibmcloud-ac-environment-get-example}

To get an environment with ID `prodEnvironment`, run the following command:

```sh
ibmcloud ac environment get --environment_id prodEnvironment
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-environment-get-output}

The command returns the following output:

```sh
name             Production_Environment
environment_id   prodEnvironment
```
{: screen}

## ibmcloud ac environment update
{: #ac-ibmcloud-ac-environment-update}

You can update an environment by using the command:

```sh
ibmcloud ac environment update (--file FILE-PATH | --environment_id ENVIRONMENT_ID --name NAME --description DESCRIPTION --tags TAGS --color_code COLOR_CODE)
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-environment-update-command}

`--name NAME`
:  Environment name. Required field - input either as a flag or from file.

`--environment_id ENVIRONMENT_ID` (optional)
:  Environment ID. Required field - input either as a flag or from file.

`--description DESCRIPTION` (optional)
:  Description of the environment. Required field - input either as a flag or from file.

`--tags TAGS` (optional)
:  Tags associated with the environment. Required field - input either as a flag or from file.

`--color_code COLOR_CODE` (optional)
:  Color code to distinguish the environment. The Hex code for the color. Required field - input either as a flag or from file.

`--file FILE`
:  Input through the file. File format Supported - JSON

### Example
{: #ac-ibmcloud-ac-environment-update-example}

To update an environment with ID `prodEnvironment` using flags ([click here](#ac-fileinput) for using commands with '--file' flag), run the following command:

```sh
ibmcloud ac environment update --name Production_Environment --environment_id prodEnvironment --description sampleUpdatedDesc --tags sampleUpdatedTag --color_code "#FF0000"
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-environment-update-output}

The command returns the following output:

```sh
name             Production_Environment
environment_id   prodEnvironment
description      sampleUpdatedDesc
tags             sampleUpdatedTag
color_code       #FF0000
created_time     2021-05-21T05:28:07.000Z
updated_time     2021-05-21T05:33:00.000Z
```
{: screen}

## ibmcloud ac environment delete
{: #ac-ibmcloud-ac-environment-delete}

You can delete an environment by using the command:

```sh
ibmcloud ac environment delete --environment_id ENVIRONMENT_ID
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-environment-delete-command}

`--environment_id ENVIRONMENT_ID`
:  Environment ID.

### Example
{: #ac-ibmcloud-ac-environment-delete-example}

To delete an environment with ID `prodEnvironment`, run the following command:

```sh
ibmcloud ac environment delete --environment_id prodEnvironment
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-environment-delete-output}

The command returns the following output:

```sh
OK
```
{: screen}

## ibmcloud ac collection list
{: #ac-ibmcloud-ac-collection-list}

You can list all collections, by using the command:

```sh
ibmcloud ac collection list [--sort SORT] [--limit LIMIT] [--offset OFFSET] [--features FEATURES] [--properties PROPERTIES] [--tags TAGS] [--expand EXPAND] [--include INCLUDE]
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-collection-list-command-options}

`--limit LIMIT` (optional)
:  Used for pagination. The number of records to retrieve.

`--offset OFFSET` (optional)
:  Used for pagination. The number of records to skip.

`--features FEATURES` (optional)
:  Filter collections by a list of comma-separated features.

`--properties PROPERTIES` (optional)
:  Filter collections by a list of comma-separated properties.

`--tags TAGS` (optional)
:  Filter based on the tags.

`--sort SORT` (optional)
:  Sort the details based on the specified attribute.

`--expand EXPAND` (optional)
:  Expanded view of the item.

`--include INCLUDE` (optional)
:  Include feature and property details in the response.

### Example
{: #ac-ibmcloud-ac-collection-list-example}

To list all collections, run the following command:

```sh
ibmcloud ac collection list
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-collection-list-output}

The command returns the following output:

```sh
name                 collection_id
sample               sampleId
GHz Inc              ghzinc1
```
{: screen}

## ibmcloud ac collection create
{: #ac-ibmcloud-ac-collection-create}

You can create a collection by using the command:

```sh
ibmcloud ac collection create {--file FILE-PATH | --name NAME [--collection_id COLLECTION_ID] [--description DESCRIPTION] [--tags TAGS]}
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-collection-create-command}

`--name NAME`
:  Collection name. Required field - input either as a flag or from file.

`--collection_id COLLECTION_ID` (optional)
:  Collection ID. If this value is not provided, the name will automatically become the ID. Optional field - input either as a flag or from file.

`--description DESCRIPTION` (optional)
:  Description of the collection. Optional field - input either as a flag or from file.

`--tags TAGS` (optional)
:  Tags associated with the collection. Optional field - input either as a flag or from file.

`--file FILE`
:  Input through the file. File format Supported - JSON

### Example
{: #ac-ibmcloud-ac-collection-create-example}

To create a collection with name `sample` using flags ([click here](#ac-fileinput) for using commands with `--file` flag), run the following command:

```sh
ibmcloud ac collection create --name sample --collection_id sampleId --description sampleDesc --tags sampleTag
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-collection-create-output}

The command returns the following output:

```sh
collection_id   sampleId
description     sampleDesc
created_time    2021-01-18T08:15:45Z
updated_time    2021-01-18T08:15:45Z
name            sample
```
{: screen}

## ibmcloud ac collection get
{: #ac-ibmcloud-ac-collection-get}

You can get a collection by using the command:

```sh
ibmcloud ac collection get --collection_id COLLECTION_ID [--expand EXPAND] [--include INCLUDE]
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-collection-get-command}

`--collection_id COLLECTION_ID`
:  Collection ID for the collection.

`--expand EXPAND` (optional)
:  Expanded view of the collection details.

`--include INCLUDE` (optional)
:  Include feature and property details in the response.

### Example
{: #ac-ibmcloud-ac-collection-get-example}

To get a collection with ID `sampleId`, run the following command:

```sh
ibmcloud ac collection get --collection_id sampleId
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-collection-get-output}

The command returns the following output:

```sh
name            sample
collection_id   sampleId
```
{: screen}

## ibmcloud ac collection update
{: #ac-ibmcloud-ac-collection-update}

You can update a collection by using the command:

```sh
ibmcloud ac collection update {--file FILE-PATH | --name NAME --collection_id COLLECTION_ID --description DESCRIPTION --tags TAGS}
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-collection-update-command}

`--collection_id COLLECTION_ID`
:  Collection ID. Required field - input either as a flag or from file.

`--name NAME`
:  Collection name. Required field - input either as a flag or from file.

`--description DESCRIPTION`
:  Description of the collection. Required field - input either as a flag or from file.

`--tags TAGS` (optional) File format Supported
:  Tags associated with the collection. Required field - input either as a flag or from file.

`--file FILE`
:  Input from the file. File format Supported - JSON

### Example
{: #ac-ibmcloud-ac-collection-update-example}

To update a collection with ID `sampleId` using flags ([click here](#ac-fileinput) for using commands with '--file' flag), run the following command:

```sh
ibmcloud ac collection update --collection_id sampleId --name sample --description sampleDesc --tags sampleTag
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-collection-update-output}

The command returns the following output:

```sh
name            sample
collection_id   sampleId
description     sampleDescUpdated
created_time    2021-01-18T08:15:45Z
updated_time    2021-01-19T05:57:27Z
```
{: screen}

## ibmcloud ac collection delete
{: #ac-ibmcloud-ac-collection-delete}

You can delete a collection by using the command:

```sh
ibmcloud ac collection delete --collection_id COLLECTION_ID
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-collection-delete-command}

`--collection_id COLLECTION_ID`
:  Collection ID

### Example
{: #ac-ibmcloud-ac-collection-delete-example}

To delete a collection with ID `sampleId`, run the following command:

```sh
ibmcloud ac collection delete --collection_id sampleId
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-collection-delete-output}

The command returns the following output:

```sh
OK
```
{: screen}

## ibmcloud ac feature list
{: #ac-ibmcloud-ac-feature-list}

You can list all features, by using the command:

```sh
ibmcloud ac feature list --environment_id ENVIRONMENT_ID [--sort SORT] [--limit LIMIT] [--offset OFFSET] [--tags TAGS] [--collections COLLECTIONS] [--segments SEGMENTS] [--expand EXPAND] [--include INCLUDE]
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-feature-list-command}

`--environment_id ENVIRONMENT_ID`
:  Environment ID

`--limit LIMIT` (optional)
:  Used for pagination. The number of records to retrieve.

`--include INCLUDE` (optional)
:  Feature details to include the associated collections or rules details in the response.

`--offset OFFSET` (optional)
:  Used for pagination. The number of records to skip.

`--collections COLLECTIONS` (optional)
:  Filter features by a list of comma-separated collections.

`--segments SEGMENTS` (optional)
:  Filter features by a list of comma-separated segments.

`--expand EXPAND` (optional)
:  Expanded view of the item.

`--tags TAGS` (optional)
:  Filter features by a list of comma-separated tags.

`--sort SORT` (optional)
:  Sort the details based on the specified attribute.

### Example
{: #ac-ibmcloud-ac-feature-list-example}

To list all features, run the following command:

```sh
ibmcloud ac feature list --environment_id "production"
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-feature-list-output}

The command returns the following output:

```sh
name            feature_id      segment_exists
Indian IBMers   ibm-discount    true
sampleFeature   sampleFeature   true
Cycle Rentals   cycle-rentals   true
```
{: screen}

## ibmcloud ac feature create
{: #ac-ibmcloud-ac-feature-create}

You can create a feature by using the command:

```sh
ibmcloud ac feature create {--file FILE-PATH | --environment_id ENVIRONMENT_ID --name NAME [--feature_id FEATURE_ID] --description DESCRIPTION --type TYPE --enabled_value ENABLED_VALUE --disabled_value DISABLED_VALUE --tags TAGS --enabled ENABLED --segment_rules SEGMENT_RULES --collections COLLECTIONS}
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-feature-create-command}

`--environment_id ENVIRONMENT_ID`
:  Environment ID

`--name NAME`
:  Feature name. Required field - input either as a flag or from file.

`--feature_id FEATURE_ID` (optional)
:  Feature ID. If this value is not provided, the name will automatically become the ID. Optional field - input either as a flag or from file.

`--description DESCRIPTION`
:  Description of the feature. Required field - input either as a flag or from file.

`--type TYPE`
:  Type of the feature (Boolean, String, Number). Required field - input either as a flag or from file.

`--enabled_value ENABLED_VALUE`
:  Value of the feature when it is enabled. Required field - input either as a flag or from file.

`--disabled_value DISABLED_VALUE`
:  Value of the feature when it is disabled. Required field - input either as a flag or from file.

`--tags TAGS`
:  Tags associated with the feature. Required field - input either as a flag or from file.

`--segment_rules SEGMENT_RULES`
:  Specify the targeting rules that are used to set different values for different segments.

`--enabled ENABLED`
:  The state of the feature flag.

`--collections COLLECTIONS`
:  Collections array.

`--file FILE`
:  Input through file. File format Supported - JSON

### Example
{: #ac-ibmcloud-ac-feature-create-example}

To create a collection with name `sample` using flags ([click here](#ac-fileinput) for using commands with '--file' flag), run the following command:

```sh
ibmcloud ac feature create --environment_id "production" --name "IBMers" --feature_id "ibm-discount" --description "Discount given to IBM employees" --type "BOOLEAN" --enabled_value true --disabled_value false --segment_rules '[{"rules":[{"segments":["ibm_employees"]}],"value": true,"order": 1}]' --collections '[{"collection_id":"corporatediscount","enabled": true}]'  --tags "discount,sale" --enabled true
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-feature-create-output}

The command returns the following output:

```sh
type             BOOLEAN
enabled_value    true
segment_rules    <Array>
collections      <Array>
name             IBMers
feature_id       ibm-discount
description      Discount given to IBM employees
disabled_value   false
enabled          true
created_time     2021-02-02T17:52:46Z
updated_time     2021-02-02T17:52:46Z
```
{: screen}

## ibmcloud ac feature get
{: #ac-ibmcloud-ac-feature-get}

You can get a feature by using the command:

```sh
ibmcloud ac feature get --environment_id ENVIRONMENT_ID --feature_id FEATURE_ID [--include INCLUDE]
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-feature-get-command}

`--environment_id ENVIRONMENT_ID`
:  Environment ID

`--feature_id FEATURE_ID`
:  Feature ID for the feature flag.

`--include INCLUDE` (optional)
:  Include the associated collections in the response.

### Example
{: #ac-ibmcloud-ac-feature-get-example}

To get a feature with ID `ibm-discount`, run the following command:

```sh
ibmcloud ac feature get --environment_id "production" --feature_id ibm-discount
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-feature-get-output}

The command returns the following output:

```sh
name    type     disabled_value  updated_time          feature_id    description                      enabled_value  created_time          order  rules    value
IBMers  BOOLEAN  false           2021-02-02T17:52:46Z  ibm-discount  Discount given to IBM employees  true           2021-02-02T17:52:46Z  1      <Array>  true
```
{: screen}

## ibmcloud ac feature update
{: #ac-ibmcloud-ac-feature-update}

You can update a feature by using the command:

```sh
ibmcloud ac feature update {--file FILE-PATH | --environment_id ENVIRONMENT_ID --name NAME --feature_id FEATURE_ID --description DESCRIPTION --enabled_value ENABLED_VALUE --disabled_value DISABLED_VALUE --enabled ENABLED --tags TAGS --segment_rules SEGMENT_RULES --collections COLLECTIONS}
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-feature-update-command}

`--environment_id ENVIRONMENT_ID`
:  Environment ID

`--name NAME`
:  Feature name. Required field - input either as a flag or from file.

`--feature_id FEATURE_ID`
:  Feature ID. Required field - input either as a flag or from file.

`--description DESCRIPTION`
:  Description of the feature. Required field - input either as a flag or from file.

`--enabled_value ENABLED_VALUE`
:  Value of the feature when it is enabled. Required field - input either as a flag or from file.

`--disabled_value DISABLED_VALUE`
:  Value of the feature when it is disabled. Required field - input either as a flag or from file.

`--tags TAGS`
:  Tags associated with the feature. Required field - input either as a flag or from file.

`--enabled ENABLED`
:  The state of the feature flag.

`--segment_rules SEGMENT_RULES`
:  Specify the targeting rules that are used to set different values for different segments.

`--collections COLLECTIONS`
:  Collections array.

`--file FILE`
:  Input through the file. File format Supported - JSON.

### Example
{: #ac-ibmcloud-ac-feature-update-example}

To update description a feature with ID `ibm-discount` using flags ([click here](#ac-fileinput) for using commands with '--file' flag), run the following command:

```sh
ibmcloud ac feature update --environment_id "production" --name "Indian IBMers" --feature_id "ibm-discount" --description "Discount given to IBM Indian employees" --enabled_value true --disabled_value false --segment_rules '[{"rules":[{"segments":["ibm_employees"]}],"value": true,"order": 1}]' --collections '[{"collection_id":"corporatediscount","enabled": true}]'  --tags "discount,sale" --enabled true
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-feature-update-output}

The command returns the following output:

```sh
updated_time     2021-02-02T18:06:03Z
description      Discount given to IBM Indian employees
enabled_value    true
disabled_value   false
segment_rules    <Array>
created_time     2021-02-02T17:52:46Z
name             Indian IBMers
type             BOOLEAN
enabled          true
collections      <Array>
```
{: screen}

## ibmcloud ac feature update-values
{: #ac-ibmcloud-ac-feature-patch}

You can update values of a feature (This method allows the update of feature name, feature enabled_value, feature disabled_value, tags, description, and feature segment rules, however this method does not allow toggling the feature flag and assigning feature to a collection.), by using the command:

```sh
ibmcloud ac feature update-values {--file FILE-PATH | --environment_id ENVIRONMENT_ID --name NAME --feature_id FEATURE_ID --description DESCRIPTION --enabled_value ENABLED_VALUE --disabled_value DISABLED_VALUE --tags TAGS --segment_rules SEGMENT_RULES}
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-feature-patch-command}

`--environment_id ENVIRONMENT_ID`
:  Environment ID

`--name NAME`
:  Feature name. Required field - input either as a flag or from file.

`--feature_id FEATURE_ID`
:  Feature ID. Required field - input either as a flag or from file.

`--description DESCRIPTION`
:  Description of the feature. Required field - input either as a flag or from file.

`--enabled_value ENABLED_VALUE`
:  Value of the feature when it is enabled. Required field - input either as a flag or from file.

`--disabled_value DISABLED_VALUE`
:  Value of the feature when it is unavailable. Required field - input either as a flag or from file.

`--tags TAGS`
:  Tags associated with the feature. Required field - input either as a flag or from file.

`--segment_rules SEGMENT_RULES`
:  Specify the targeting rules that are used to set different values for different segments.

`--file FILE`
:  Input through the file. File format Supported - JSON

### Example
{: #ac-ibmcloud-ac-feature-patch-example}

To update description a feature with ID `ibm-discount` using flags ([click here](#ac-fileinput) for using commands with '--file' flag), run the following command:

```sh
ibmcloud ac feature update-values --environment_id "production" --name "Indian IBMers" --feature_id "ibm-discount" --description "Discount given to IBM Indian employees" --enabled_value true --disabled_value false --segment_rules '[{"rules":[{"segments":["ibm_employees"]}],"value": true,"order": 1}]'  --tags "discount,sale"
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-feature-patch-output}

The command returns the following output:

```sh
updated_time     2021-02-02T18:06:03Z
description      Discount given to IBM Indian employees
enabled_value    true
disabled_value   false
segment_rules    <Array>
created_time     2021-02-02T17:52:46Z
name             Indian IBMers
type             BOOLEAN
collections      <Array>
```
{: screen}

## ibmcloud ac feature delete
{: #ac-delete}

You can delete a feature by using the command:

```sh
ibmcloud ac feature delete --environment_id ENVIRONMENT_ID --feature_id FEATURE_ID
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-feature-delete-command}

`--environment_id ENVIRONMENT_ID`
:  Environment ID

`--feature_id FEATURE_ID`
:  Feature ID

### Example
{: #ac-delete-example}

To delete a feature with ID `ibm-discount`, run the following command:

```sh
ibmcloud ac feature delete --environment_id "production" --feature_id ibm-discount
```
{: pre}

#### Output
{: #ac-delete-output}

The command returns the following output:

```sh
OK
```
{: screen}

## ibmcloud ac feature toggle
{: #ac-ibmcloud-ac-feature-toggle}

You can toggle a feature value by using the command:

```sh
ibmcloud ac feature toggle --environment_id ENVIRONMENT_ID --feature_id FEATURE_ID --enabled ENABLED
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-feature-toggle-command}

`--environment_id ENVIRONMENT_ID`
:  Environment ID

`--feature_id FEATURE_ID`
:  Feature ID

`--enabled ENABLED`
:  The state of the feature flag.

### Example
{: #ac-ibmcloud-ac-feature-toggle-example}

To toggle a feature value with ID `ibm-discount`, run the following command:

```sh
ibmcloud ac feature toggle --environment_id "production" --feature_id ibm-discount --enabled false
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-feature-delete-output}

The command returns the following output:

```sh
name    type     disabled_value  updated_time          feature_id    description                      enabled_value  created_time          order  rules    value
IBMers  BOOLEAN  false           2021-02-02T17:52:46Z  ibm-discount  Discount given to IBM employees  true           2021-02-02T17:52:46Z  1      <Array>  true
```
{: screen}

## ibmcloud ac segment list
{: #ac-ibmcloud-ac-segment-list}

You can list all segments, by using the command:

```sh
ibmcloud ac segment list [--limit LIMIT] [--offset OFFSET] [--sort SORT] [--tags TAGS] [--expand EXPAND] [--include INCLUDE]
```
{: pre}

### Command options
{: #ac-command}

`--limit LIMIT` (optional)
:  Used for pagination. The number of records to retrieve.

`--include INCLUDE` (optional)
:  Segment details to include the associated rules in the response.

`--offset OFFSET` (optional)
:  Used for pagination. The number of records to skip.

`--expand EXPAND` (optional)
:  Expanded view the segment details.

`--tags TAGS` (optional)
:  Filter segments by a list of comma-separated tags.

`--sort SORT` (optional)
:  Sort the details based on the specified attribute.

### Example
{: #ac-example}

To list all segments, run the following command:

```sh
ibmcloud ac segment list
```
{: pre}

#### Output
{: #ac-output}

The command returns the following output:

```sh
name            segment_id
India IBMers    ibm_employees_01
IBM Employees   ibm_employees
```
{: screen}

## ibmcloud ac segment create
{: #ac-create}

You can create a segment by using the command:

```sh
ibmcloud ac segment create {--file FILE-PATH | --name NAME [--segment_id SEGMENT_ID] --description DESCRIPTION --tags TAGS --rules RULES}
```
{: pre}

### Command options
{: #ac-create-command}

`--name NAME`
:  Segment name. Required field - input either as a flag or from file.

`--segment_id SEGMENT_ID` (optional)
:  Segment ID. If this value is not provided, the name will automatically become the ID. Optional field - input either as a flag or from file.

`--description DESCRIPTION`
:  Description of the segment. Required field - input either as a flag or from file.

`--rules RULES`
:  List of rules that determine whether the entity is part of the segment. Required field - input either as a flag or from file.

`--tags TAGS`
:  Tags associated with the segment. Required field - input either as a flag or from file.

`--file FILE`
:  Input through a file. File format Supported - JSON

### Example
{: #ac-create-example}

To create a collection with name `sample` using flags ([click here](#ac-fileinput) for using commands with '--file' flag), run the following command:

```sh
ibmcloud ac segment create --name "IBM Employees" --segment_id "ibm_employees" --description "IBM Employees Segment" --tags "ibm" --rules '[{"attribute_name": "email", "operator": "endsWith", "values": ["@ibm.com"]}]'
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-segment-create-output}

The command returns the following output:

```sh
name           IBM Employees
segment_id     ibm_employees
description    IBM Employees Segment
created_time   2021-02-02T19:04:22Z
updated_time   2021-02-02T19:04:22Z
```
{: screen}

## ibmcloud ac segment get
{: #ac-ibmcloud-ac-segment-get}

You can get a segment by using the command:

```sh
ibmcloud ac segment get --segment_id SEGMENT_ID [--include INCLUDE]
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-segment-get-command}

`--segment_id SEGMENT_ID`
:  Segment ID.

`--include INCLUDE` (optional)
:  Instructs to include the feature and property details based on the segments association.

### Example
{: #ac-ibmcloud-ac-segment-get-example}

To get a segment with ID `ibm_employees`, run the following command:

```sh
ibmcloud ac segment get --segment_id ibm_employees
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-segment-get-output}

The command returns the following output:

```sh
segment_id     description    features  created_time          updated_time          name           attribute_name  operator  values
ibm_employees  IBM Employees  -         2021-02-02T19:04:22Z  2021-02-02T19:04:22Z  IBM Employees  email           endsWith  <Array>
```
{: screen}

## ibmcloud ac segment update
{: #ac-ibmcloud-ac-segment-update}

You can update a segment by using the command:

```sh
ibmcloud ac segment update {--file FILE-PATH | --name NAME --segment_id SEGMENT_ID --description DESCRIPTION --tags TAGS --rules RULES}
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-segment-update-command}

`--name NAME`
:  Segment name. Required field - input either as a flag or from file.

`--segment_id SEGMENT_ID`
:  Segment ID. Required field - input either as a flag or from file.

`--description DESCRIPTION`
:  Description of the segment. Required field - input either as a flag or from file.

`--rules RULES`
:  List of rules that determine whether the entity is part of the segment. Required field - input either as a flag or from file.

`--tags TAGS`
:  Tags associated with the segment. Required field - input either as a flag or from file.

`--file FILE`
:  Input through a file. File format Supported - JSON

### Example
{: #ac-ibmcloud-ac-segment-update-example}

To update description a segment with ID `ibm_employees` using flags ([click here](#ac-fileinput) for using commands with '--file' flag), run the following command:

```sh
ibmcloud ac segment update --name "IBM India Employees" --segment_id "ibm_employees" --description "IBM India Employees" --tags "ibm" --rules '[{"attribute_name": "email", "operator": "endsWith", "values": ["@in.ibm.com"]}]'
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-segment-update-output}

The command returns the following output:

```sh
description    IBM India Employees
created_time   2021-02-02T19:04:22Z
updated_time   2021-02-02T19:10:01Z
name           IBM India Employees
segment_id     ibm_employees
```
{: screen}

## ibmcloud ac segment delete
{: #ac-ibmcloud-ac-segment-delete}

You can delete a segment by using the command:

```sh
ibmcloud ac segment delete --segment_id SEGMENT_ID
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-segment-delete-command}

`--segment_id SEGMENT_ID`
:  Segment ID

### Example
{: #ac-ibmcloud-ac-segment-delete-example}

To delete a segment with ID `ibm_employees`, run the following command:

```sh
ibmcloud ac segment delete --segment_id ibm_employees
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-segment-delete-output}

The command returns the following output:

```sh
OK
```
{: screen}

## ibmcloud ac property list
{: #ac-ibmcloud-ac-property-list}

You can list all properties, by using the command:

```sh
ibmcloud ac property list --environment_id ENVIRONMENT_ID [--expand EXPAND] [--sort SORT] [--tags TAGS] [--include INCLUDE] [--collections COLLECTIONS] [--segments SEGMENTS] [--limit LIMIT] [--offset OFFSET]
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-property-list-command}

`--environment_id ENVIRONMENT_ID`
:  Environment ID

`--limit LIMIT` (optional)
:  Used for pagination. The number of records to retrieve.

`--include INCLUDE` (optional)
:  Segment details to include the associated rules in the response.

`--offset OFFSET` (optional)
:  Used for pagination. The number of records to skip.

`--collections COLLECTIONS` (optional)
:  Filter features by a list of comma-separated collections.

`--segments SEGMENTS` (optional)
:  Filter features by a list of comma-separated segments.

`--expand EXPAND` (optional)
:  Expanded view the segment details.

`--tags TAGS` (optional)
:  Filter segments by a list of comma-separated tags.

`--sort SORT` (optional)
:  Sort the details based on the specified attribute.

### Example
{: #ac-ibmcloud-ac-property-list-example}

To list all properties, run the following command:

```sh
ibmcloud ac property list --environment_id "production"
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-property-list-output}

The command returns the following output:

```sh
collections   name             property_id      description                 type      value   tags                        segment_rules
-             Email property   email-property   Property for email Update   BOOLEAN   false   version: 1.1, pre-release   -
-             name             name             desc                        NUMERIC   1       tags                        -
```
{: screen}

## ibmcloud ac property create
{: #ac-ibmcloud-ac-property-create}

You can create a property by using the command:

```sh
ibmcloud ac property create (--file FILE-PATH | --environment_id ENVIRONMENT_ID --name NAME [--property_id PROPERTY_ID] --description DESCRIPTION --type TYPE --value VALUE --tags TAGS --segment_rules SEGMENT-RULES --collections COLLECTIONS)
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-property-create-command}

`--environment_id ENVIRONMENT_ID`
:  Environment ID

`--name NAME`
:  Property name. Required field - input either as a flag or from file.

`--property_id PROPERTY_ID` (optional)
:  Property ID. If this value is not provided, the name will automatically become the ID. Optional field - input either as a flag or from file.

`--description DESCRIPTION`
:  Description of the property. Required field - input either as a flag or from file.

`--segment_rules SEGMENT_RULES`
:  Specify the targeting rules that are used to set different values for different segments. Required field - input either as a flag or from file.

`--tags TAGS`
:  Tags associated with the property. Required field - input either as a flag or from file.

`--value VALUE`
:  Property value. Required field - input either as a flag or from file.

`--type TYPE`
:  Property type. Required field - input either as a flag or from file.

`--collections COLLECTIONS`
:  List of collection IDs representing the collections that are associated with the specified property. Required field - input either as a flag or from file.

`--file FILE`
:  Input through a file. File format Supported - JSON

### Example
{: #ac-ibmcloud-ac-property-create-example}

To create a property with name `email-property` using flags ([click here](#ac-fileinput) for using commands with '--file' flag), run the following command:

```sh
ibmcloud ac property create --environment_id "production" --name Email_Property --property_id email-property --description Email_Property --type STRING --value VALUE --tags tags --segment_rules '[{"rules":[{"segments":["kmu9n7px"]}],"value":"$default","order":1}]' --collections '[]'
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-property-create-output}

The command returns the following output:

```sh
name             Email_Property
description      Email_Property
type             STRING
value            VALUE
segment_rules    <Array>
property_id      email-property
segment_exists   true
tags             tags
collections      -
```
{: screen}

## ibmcloud ac property get
{: #ac-ibmcloud-ac-property-get}

You can get a property by using the command:

```sh
ibmcloud ac property get --environment_id ENVIRONMENT_ID --property_id PROPERTY_ID [--include INCLUDE]
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-property-get-command}

`--environment_id ENVIRONMENT_ID`
:  Environment ID

`--property_id PROPERTY_ID`
:  Property ID for the property flag.

`--include INCLUDE` (optional)
:  Property details to include the associated collections or rules details in the response.

### Example
{: #ac-ibmcloud-ac-property-get-example}

To get a property with ID `email-property`, run the following command:

```sh
ibmcloud ac property get --environment_id "production" --property_id email-property
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-property-get-output}

The command returns the following output:

```sh
tags                        collections   name             property_id      description                 type      value   rules     value   order
version: 1.1, pre-release   -             Email_Property   email-property   Property for email Update   BOOLEAN   false   <Array>   true    1
```
{: screen}

## ibmcloud ac property update
{: #ac-ibmcloud-ac-property-update}

You can update a property by using the command:

```sh
ibmcloud ac property update (--file FILE-PATH | --environment_id ENVIRONMENT_ID --property_id PROPERTY_ID [--name NAME] [--description DESCRIPTION] [--value VALUE] [--tags TAGS] [--segment_rules SEGMENT-RULES] [--collections COLLECTIONS])
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-property-update-command}

`--environment_id ENVIRONMENT_ID`
:  Environment ID

`--name NAME`
:  Property name. Required field - input either as a flag or from file.

`--property_id PROPERTY_ID`
:  Property ID. Required field - input either as a flag or from file.

`--description DESCRIPTION`
:  Description of the property. Required field - input either as a flag or from file.

`--segment_rules SEGMENT_RULES`
:  Specify the targeting rules that are used to set different values for different segments. Required field - input either as a flag or from file.

`--tags TAGS`
:  Tags associated with the property. Required field - input either as a flag or from file.

`--value VALUE`
:  Property value. Required field - input either as a flag or from file.

`--collections COLLECTIONS`
:  List of collection IDs representing the collections that are associated with the specified property. Required field - input either as a flag or from file.

`--file FILE`
:  Input through a file. File format Supported - JSON

### Example
{: #ac-ibmcloud-ac-property-update-example}

To update description a property with ID `email-property` using flags ([click here](#ac-fileinput) for using commands with '--file' flag), run the following command:

```sh
ibmcloud ac property update --environment_id "production" --name Email_Property --property_id email-property --description Email_Property_Updated --value VALUE --tags Updated_Tags --segment_rules '[{"rules":[{"segments":["kmu9n7px"]}],"value":"$default","order":1}]' --collections '[]'
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-property-update-output}

The command returns the following output:

```sh
name             Email_Property
value            VALUE
segment_rules    <Array>
collections      -
tags             Updated_Tags
property_id      email-property
segment_exists   true
description      Email_Property_Updated
type             STRING
```
{: screen}

## ibmcloud ac property update-values
{: #ac-ibmcloud-ac-property-patch}

You can update the property values(Property value and targeting rules can be updated, however this method does not allow assigning property to a collection.), by using the command:

```sh
ibmcloud ac property update-values (--file FILE-PATH | --environment_id ENVIRONMENT_ID --property_id PROPERTY_ID [--name NAME] [--description DESCRIPTION][--value VALUE] [--tags TAGS] [--segment_rules SEGMENT-RULES])
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-property-patch-command}

`--environment_id ENVIRONMENT_ID`
:  Environment ID

`--name NAME`
:  Property name. Required field - input either as a flag or from file.

`--property_id PROPERTY_ID`
:  Property ID. Required field - input either as a flag or from file.

`--description DESCRIPTION`
:  Description of the property. Required field - input either as a flag or from file.

`--segment_rules SEGMENT_RULES`
:  Specify the targeting rules that are used to set different values for different segments. Required field - input either as a flag or from file.

`--tags TAGS`
:  Tags associated with the property. Required field - input either as a flag or from file.

`--value VALUE`
:  Property value. Required field - input either as a flag or from file.

`--file FILE`
:  Input through file. File format Supported - JSON

### Example
{: #ac-ibmcloud-ac-property-patch-example}

To update description of a property with ID `email-property` using flags ([click here](#ac-fileinput) for using commands with '--file' flag), run the following command:

```sh
ibmcloud ac property update-values --environment_id "production" --name Email_Property --property_id email-property --description Email_Property_Updated --value VALUE --tags Updated_Tags --segment_rules '[{"rules":[{"segments":["kmu9n7px"]}],"value":"$default","order":1}]'
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-property-patch-output}

The command returns the following output:

```sh
name             Email_Property
value            VALUE
segment_rules    <Array>
tags             Updated_Tags
property_id      email-property
segment_exists   true
description      Email_Property_Updated
type             STRING
```
{: screen}

## ibmcloud ac property delete
{: #ac-ibmcloud-ac-property-delete}

You can delete a property by using the command:

```sh
ibmcloud ac property delete --environment_id ENVIRONMENT_ID --property_id PROPERTY_ID
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-property-delete-command}

`--environment_id ENVIRONMENT_ID`
:  Environment ID

`--property_id PROPERTY_ID`
:  Property ID

### Example
{: #ac-ibmcloud-ac-property-delete-example}

To delete a property with ID `ibm_employees`, run the following command:

```sh
ibmcloud ac property delete --environment_id "production" --property_id ibm_employees
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-property-delete-output}

The command returns the following output:

```sh
OK
```
{: screen}

## ibmcloud ac export
{: #ac-ibmcloud-ac-export}

You can export configuration data of the selected instance, by using the command:

```sh
ibmcloud ac export [--file FILE] [--output OUTPUT]
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-export-command}

`--file FILE` (optional)
:  Path of file to where the configuration will be exported.

`--output OUTPUT` (optional)
:  Choose an output format - this can be 'JSON' or 'yaml'. (default "JSON")

### Example
{: #ac-ibmcloud-ac-export-example}

To export configuration data of the selected instance, run the following command:

```sh
ibmcloud ac export --file exportedConfig.json
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-export-output}

The command returns the following output:

```sh
OK
Configuration exported to file exportedConfig.json
```
{: screen}

## ibmcloud ac import
{: #ac-ibmcloud-ac-import}

You can import configuration data from a file to the selected instance, by using the command:

```sh
ibmcloud ac import --file FILE [--clean CLEAN]
```
{: pre}

### Command options
{: #ac-ibmcloud-ac-import-command}

`--file FILE`
:  Path of the file from where the configuration will be imported.

`--clean CLEAN` (optional)
:  If set to 'true', clears the existing data in the service instance before the import of the configuration data.

### Example
{: #ac-ibmcloud-ac-import-example}

To import configuration data from a file to the selected instance, run the following command:

```sh
ibmcloud ac import --file exportedConfig.json
```
{: pre}

#### Output
{: #ac-ibmcloud-ac-import-output}

The command returns the following output:

```sh
OK
Configuration imported from file exportedConfig.json
```
{: screen}

## Creating or Updating an item from file
{: #ac-fileinput}

The plug-in provides you with the functions of creating or updating items in JSON format that is stored in a file.

This is how you can create collection from a file.

```sh
ibmcloud ac collection create {--file FILE-PATH | --name NAME [--collection_id COLLECTION_ID] [--description DESCRIPTION] [--tags TAGS]}
```
{: pre}

Notice the '|' symbol. This indicates that there are two ways to use the command.

```sh
ibmcloud ac collection create --file FILE-PATH
OR
ibmcloud ac collection create --name NAME [--collection_id COLLECTION_ID] [--description DESCRIPTION] [--tags TAGS]
```
{: codeblock}

To view the supported JSON format, see the [API Docs](/apidocs/app-configuration).

Use the file flag (cannot be combined with any other flag) to give the path of the file.

### Example
{: #ac-fileinput-example}

To create a collection with ID `corporateDiscount` stored in a file *create_collection_body.json*, run the following command:

```sh
ibmcloud ac collection create --file create_collection_body.json
```
{: pre}

Here is the content of `create_collection_body.json`:

```sh
{
    "name": "Corporate Discount",
    "collection_id": "corporateDiscount",
    "description": "Discount for partner Organizations",
    "tags": "discount,sale"
}
```
{: codeblock}

#### Output
{: #ac-fileinput-output}

The command returns the following output:

```sh
name            Corporate Discount
collection_id   corporateDiscount
description     Discount for partner Organizations
created_time    2021-02-02T19:17:07Z
updated_time    2021-02-02T19:17:07Z
```
{: screen}

The behavior for create and update of a collection or feature or segment is similar as mentioned earlier. For accepted JSON format structure, see the [API Docs](/apidocs/app-configuration)

## ibmcloud plug-in uninstall
{: #ac-ibmcloud-plugin-uninstall}

Use this command to uninstall the App Configuration CLI plug-in.

```sh
ibmcloud plugin uninstall app-configuration
```
{: pre}

Uninstall returns a success message, if no errors.
