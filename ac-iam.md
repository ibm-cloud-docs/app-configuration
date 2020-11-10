---

copyright:
  years: 2020
lastupdated: "2020-11-10"

keywords: app-configuration, app configuration, managing service access, iam, account

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

# Managing service access
{: #ac-service-access-management}

{{site.data.keyword.appconfig_short}} uses {{site.data.keyword.iamlong}} (IAM) to perform authorization and authentication.
{: shortdesc}

Access to {{site.data.keyword.appconfig_short}} service instances for users in your account is controlled by {{site.data.keyword.iamlong}} (IAM). Every user in your account, who needs access to {{site.data.keyword.appconfig_short}}, must be assigned with an IAM role with specific access policy. The access policy determines what actions a user can perform within the context of the service or instance that you select. The allowable actions are customized and defined by the {{site.data.keyword.cloud_notm}} service as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles.

Policies help you to grant access at different levels. Some of the options are,
- Access across all instances of the service in your account.
- Access to an individual service instance in your account.
- Access to a specific resource within an instance.

## Roles and permissions
{: #ac-roles-permissions}

With {{site.data.keyword.cloud_notm}} IAM, you can manage and define access for users and resources in your account. {{site.data.keyword.appconfig_short}} service aligns with {{site.data.keyword.cloud_notm}} IAM roles so that each user has a different view of the service, according to the role assigned. 

To simplify access, if you are a security admin for your service, you can assign {{site.data.keyword.cloud_notm}} IAM roles that correspond to the specific {{site.data.keyword.cloud_notm}} service permissions you want to grant to members of your team.

For complete IAM documentation, see [Managing access](/docs/account?topic=account-cloudaccess) in {{site.data.keyword.cloud_notm}}.
{: note}

Review the available platform and service roles available and the actions that are mapped to each to help you assign access. If you're using the API to assign access, use `apprapp` for the service name.

| Role | Description |
| ----- | :----- |
| Administrator | As an administrator, you can perform all platform actions based on the resource this role is being assigned, including assigning access policies to other users. |
| Editor | As an editor, you can perform all platform actions except for managing the account and assigning access policies. |
| Operator | As an operator, you can perform platform actions that are required to configure and operate service instances, such as viewing a service's dashboard. |
| Viewer | As a viewer, you can view service instances, but you can't modify them. |
{: row-headers}
{: caption="Table 1. Platform roles - {{site.data.keyword.appconfig_short}}" caption-side="top"}
{: #platform-roles-table1}
{: tab-title="Platform roles"}
{: tab-group="app-rapp"}
{: class="simple-tab-table"}
{: summary="Use the tab buttons to change the context of the table. This table has row and column headers. The row headers provide the platform role name and the column headers identify the specific information available about each role."}

| Role | Description |
| ----- | :----- |
| Manager | All service APIs can be accessed. |
| Reader | All service APIs can be accessed. |
| Writer | All service APIs can be accessed. |
| ConfigReader | All service APIs can be accessed. |
{: row-headers}
{: caption="Table 1. Service roles - {{site.data.keyword.appconfig_short}}" caption-side="top"}
{: #service-roles-table1}
{: tab-title="Service roles"}
{: tab-group="app-rapp"}
{: class="simple-tab-table"}
{: summary="Use the tab buttons to change the context of the table. This table has row and column headers. The row headers provide the service role name and the column headers identify the specific information available about each role."}

| Action | Description | Roles |
| ----- | :----- | :----- |
| `apprapp.dashboard.view` | View {{site.data.keyword.appconfig_short}} dashboard | Manager, Reader, Writer, Operator, Administrator, Editor |
| `apprapp.apps.list` | Get list of collection. | Reader, Manager, Writer, Administrator, Editor, Viewer, Operator, ConfigReader |
| `apprapp.apps.create` | Create a collection. | Manager, Reader, Writer, Administrator, Editor, Viewer, Operator, ConfigReader |
| `apprapp.apps.update` | Update the collection name, tags, and description. | Manager, Reader, Writer, Administrator, Editor, Viewer, Operator, ConfigReader |
| `apprapp.apps.delete` | Delete the collection. | Manager, Reader, Writer, ConfigReader |
| `apprapp.features.list` | Get list of feature flags. | Manager, Reader, Writer, ConfigReader |
| `apprapp.features.create` | Create a feature flag. | Manager, Reader, Writer, ConfigReader |
| `apprapp.features.update` | Update a feature flag property. | Manager, Reader, Writer, ConfigReader |
| `apprapp.features.delete` | Delete a feature flag. | Manager, Reader, Writer, ConfigReader |
| `apprapp.segments.list` | Get list of segments. | Manager, Reader, Writer, ConfigReader |
| `apprapp.segments.create` | Create a segment of users. | Manager, Reader, Writer, ConfigReader |
| `apprapp.segments.update` | Update the segment properties. | Manager, Reader, Writer, ConfigReader |
| `apprapp.segments.delete` | Delete a segment. | Manager, Reader, Writer, ConfigReader |
{: caption="Table 1. Service actions - {{site.data.keyword.appconfig_short}}" caption-side="top"}
{: #actions-table1}
{: tab-title="Actions"}
{: tab-group="app-rapp"}
{: class="simple-tab-table"}
{: summary="Use the tab buttons to change the context of the table. This table provides the available actions for the service, descriptions of each, and the roles that each action is mapped to."}

