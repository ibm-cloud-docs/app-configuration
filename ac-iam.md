---

copyright:
  years: 2020, 2024
lastupdated: "2024-02-06"

keywords: app-configuration, app configuration, managing service access, iam, account

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Managing service access
{: #ac-service-access-management}

{{site.data.keyword.appconfig_short}} uses {{site.data.keyword.iamlong}} (IAM) to perform authorization and authentication.
{: shortdesc}

Access to {{site.data.keyword.appconfig_short}} service instances for users in your account is controlled by {{site.data.keyword.iamlong}} (IAM). Every user in your account who needs access to {{site.data.keyword.appconfig_short}}, must be assigned with an IAM role with specific access policy. The access policy determines what actions that a user can perform within the context of the service or instance that you select. The allowable actions are customized and defined by the {{site.data.keyword.cloud_notm}} service as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles.

Policies help you to grant access at different levels. Some of the options are:

- Access across all instances of the service in your account.
- Access to an individual service instance in your account.
- Access to specific Feature flags & Properties only within a Collection. [See tutorial](/docs/app-configuration?topic=app-configuration-ac-assign-access-to-collections).
- Access to all Feature flags & Properties within a specific Environment. [See tutorial](/docs/app-configuration?topic=app-configuration-ac-assign-access-to-environments).

## Roles and permissions
{: #ac-roles-permissions}

With {{site.data.keyword.cloud_notm}} IAM, you can manage and define access for users and resources in your account. {{site.data.keyword.appconfig_short}} service aligns with {{site.data.keyword.cloud_notm}} IAM roles so that each user has a different view of the service, according to the role assigned.

*Roles* define the actions that a user or service ID can run. The following types of roles are in {{site.data.keyword.cloud_notm}}:

- *Platform management roles* enable users to perform tasks on service resources at the platform level, for example assign user access for the service, create or delete service IDs, create instances, assign policies for your service to other users, or bind instances to applications.
- *Service access roles* enable users to be assigned varying levels of permission for calling the service's API.

{{site.data.keyword.appconfig_short}} uses both the **Platform and Service management roles**. You can set policies about who can create an instance at the platform level, and then use the service roles to manage interaction with the instance itself. As the creator of an instance, you do not need to set any IAM policies to view or work with your {{site.data.keyword.appconfig_short}} entities.

For complete IAM documentation, see [Managing access](/docs/account?topic=account-cloudaccess) in {{site.data.keyword.cloud_notm}}.
{: note}

Review the platform and service roles available and the actions that are mapped to each to help you assign access. If you're using the API to assign access, use `apprapp` for the service name.

| Role | Description |
| :----- | :----- |
| Viewer | As a viewer, you can view service instances, but you can't modify them. |
| Administrator | As an administrator, you can perform all platform actions based on the resource this role is being assigned, including assigning access policies to other users. |
| Operator | As an operator, you can perform platform actions that are required to configure and operate service instances, such as viewing a service's dashboard. |
| Editor | As an editor, you can perform all platform actions except for managing the account and assigning access policies. |
{: row-headers}
{: caption="Table 1. IAM user roles" caption-side="bottom"}
{: #platform-roles-table1}
{: tab-title="Platform roles"}
{: tab-group="app-rapp"}
{: class="simple-tab-table"}
{: summary="Use the tab buttons to change the context of the table. This table has row and column headers. The row headers provide the platform role name and the column headers identify the specific information available about each role."}

| Role | Description |
| :----- | :----- |
| Manager | As a manager, you have permissions beyond the writer role to complete privileged actions as defined by the service. In addition, you can create and edit service-specific resources. |
| Reader | As a reader, you can perform read-only actions within a service such as viewing service-specific resources. |
| Writer | As a writer, you have permissions beyond the reader role, including creating and editing service-specific resources. |
| Config Operator | As a Config Operator, you can toggle the feature state. |
| Client SDK | As a Client SDK role, you have permissions to perform evaluation of feature flags and properties in your application integrated with client SDK. |
{: row-headers}
{: caption="Table 2. IAM service access roles" caption-side="bottom"}
{: #service-roles-table1}
{: tab-title="Service roles"}
{: tab-group="app-rapp"}
{: class="simple-tab-table"}
{: summary="Use the tab buttons to change the context of the table. This table has row and column headers. The row headers provide the service role name and the column headers identify the specific information available about each role."}

## Actions
{: #ac-iam-actions}

The following table details actions that are mapped to service access roles. Service access roles enable users access to App Configuration as well as the ability to call the App Configuration API.

| No. | Action ID | Roles | Description |
| :---- | :----- | :----- | :----- |
| 1. | `apprapp.dashboard.view` | Manager, Writer, Config Operator, Reader | View {{site.data.keyword.appconfig_short}} dashboard |
| 2. | `apprapp.collections.list` | Manager, Writer, Config Operator, Reader, ClientSDK | The ability to view collections. |
| 3. | `apprapp.collections.create` | Manager | The ability to create collections. |
| 4. | `apprapp.collections.update` | Manager | The ability to edit or update existing collections. |
| 5. | `apprapp.collections.delete` | Manager | The ability to delete existing collections. |
| 6. | `apprapp.environments.list` | Manager, Writer, Config Operator, Reader | The ability to view environments. |
| 7. | `apprapp.environments.create` | Manager | The ability to create environments. |
| 8. | `apprapp.environments.update` | Manager | The ability to update or edit existing environments. |
| 9. | `apprapp.environments.delete` | Manager | The ability to delete existing environments. |
| 10. | `apprapp.features.list` | Manager, Writer, Config Operator, Reader | The ability to view feature flags. |
| 11. | `apprapp.features.create` | Manager | The ability to create feature flags. |
| 12. | `apprapp.features.update` | Manager | The ability to update or edit existing feature flags. |
| 13. | `apprapp.features.delete` | Manager | The ability to delete existing feature flags. |
| 14. | `apprapp.features.patch` | Writer | The ability to partially update or edit existing feature flags. |
| 15. | `apprapp.features.toggle` | Manager, Writer, Config Operator | The ability to enable or disable existing feature flags. |
| 16. | `apprapp.properties.list` | Manager, Writer, Config Operator, Reader | The ability to view properties. |
| 17. | `apprapp.properties.create` | Manager | The ability to create properties. |
| 18. | `apprapp.properties.update` | Manager | The ability to update or edit existing properties. |
| 19. | `apprapp.properties.delete` | Manager | The ability to delete existing properties. |
| 20. | `apprapp.properties.patch` | Writer | The ability to partially update or edit existing properties. |
| 21. | `apprapp.segments.list` | Manager, Writer, Config Operator, Reader | The ability to view segments. |
| 22. | `apprapp.segments.create` | Manager, Writer | The ability to create segments. |
| 23. | `apprapp.segments.update` | Manager, Writer | The ability to update or edit existing segments. |
| 24. | `apprapp.segments.delete` | Manager, Writer | The ability to delete existing segments. |
| 25. | `apprapp.gitconfigs.view` | Manager, Writer, Config Operator, Reader | The ability to view Git configurations. |
| 26. | `apprapp.gitconfigs.create` | Manager | The ability to create Git configurations. |
| 27. | `apprapp.gitconfigs.update` | Manager | The ability to update or edit existing Git configurations. |
| 28. | `apprapp.gitconfigs.delete` | Manager | The ability to delete existing Git configurations. |
| 29. | `apprapp.integrations.list` | Manager, Writer, Config Operator, Reader | The ability to view integrations existing between App Configuration service and external services such as Key Protect, HPCS & Event Notifications. |
| 30. | `apprapp.integrations.create` | Manager | The ability to create integrations between App Configuration service and external services such as Key Protect, HPCS and Event Notifications. |
| 31. | `apprapp.integrations.delete` | Manager | The ability to delete the existing integrations between App Configuration service and an external services such as Key Protect, HPCS & Event Notifications. |
| 32. | `apprapp.originconfigs.list` | Manager, Writer, Config Operator, Reader | The ability to view allowlisted origin URLs. |
| 32. | `apprapp.originconfigs.update` | Manager | The ability to add or update origin URLs to the allowlist. |
| 34. | `apprapp.workflowconfigs.list` | Manager, Writer, Config Operator, Reader | The ability to view workflow configurations. |
| 35. | `apprapp.workflowconfigs.create` | Manager | The ability to create workflow configurations. |
| 36. | `apprapp.workflowconfigs.update` | Manager | The ability to update or edit existing workflow configurations. |
| 37. | `apprapp.workflowconfigs.delete` | Manager | The ability to delete existing workflow configurations. |
| 38. | `apprapp.changerequest.create` |  Manager | The ability to send ServiceNow change request events to App Configuration instance. |
| 39. | `apprapp.config.export` | Manager, Writer, Config Operator, Reader, ClientSDK | The ability to get the JSON export of entire App Configuration instance resources such as collections, environments, feature flags, properties & segments. |
| 40. | `apprapp.config.import` | Manager | The ability to import resources such as collections, environments, feature flags, properties & segments into App Configuration instance. |
| 41. | `apprapp.config.action` | Manager | The ability to promote or restore the existing Git configurations. |
| 42. | `apprapp.sse.view` | Manager, Writer, Config Operator, Reader, ClientSDK | The ability for a EventSource to subscribe to server-sent events. This action is used by App Configuration Client SDKs only. |
| 43. | `apprapp.usage.create` | Manager, Writer, Config Operator, Reader, ClientSDK | The ability to submit feature flags & properties evaluation metrics back to App Configuration. |
{: caption="Table 3. Granular IAM action descriptions." caption-side="bottom"}
