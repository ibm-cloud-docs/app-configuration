---

copyright:
  years: 2020, 2022
lastupdated: "2022-09-30"

keywords: app-configuration, app configuration, managing service access, iam, account, environments

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Managing access levels for {{site.data.keyword.appconfig_short}} environments
{: #ac-service-access-level-management}

You can enable different levels of access to an {{site.data.keyword.appconfig_short}} environment in your {{site.data.keyword.cloud_notm}} account by creating and modifying {{site.data.keyword.iamlong}} (IAM) access policies.
{: shortdesc}

## Granting access to an environment across instances in the account
{: #ac-access-management-env}

Take the following steps on the {{site.data.keyword.cloud_notm}} console:

1. From the menu bar, click **Manage > Access (IAM)**, and select **Users** to browse the existing users in your account.

1. Select the name of the user to assign the access.

1. Click the **Access** tab in the Manager page view.

1. Click **Assign access**.

1. Select the **Access policy** if it is not already expanded.

1. From the list of services, select {{site.data.keyword.appconfig_short}}, and click **Next**.

1. Scope the access to **Specific resources**.

1. Select the **environment** attribute type and provide the environment ID as the value, and click **Next**.

1. Choose a combination of [platform and service access roles](/docs/app-configuration?topic=app-configuration-ac-service-access-management) to assign access for the user, and click **Finish**.

1. Click **Add**.

1. Repeat these steps as needed, and click **Assign**.

![Access to an environment across instances](images/rbac-env.png "Access to an environment across instances"){: caption="Figure 1. Access to an environment across instances" caption-side="bottom"}

To enable access to environments across instances, the user must at least have Reader level privileges to the {{site.data.keyword.appconfig_short}} instances in the account.
{: note}

## Granting access to a specific environment in an instance
{: #ac-access-management-instance}

Take the following steps on the {{site.data.keyword.cloud_notm}} console:

1. From the menu bar, click **Manage > Access (IAM)**, and select **Users** to browse the existing users in your account.

1. Select the name of the user to assign the access.

1. Click Access policies tab in the Manager page view.

1. Click Assign access.

1. Select the **Assign users additional access** section if it is not already expanded.

1. From the list of services, select {{site.data.keyword.appconfig_short}}.

1. Select the **Resource based on selected attributes** option.

1. Select the **serviceInstance** attribute and provide the service instance ID as the value.

1. Select the **environment** and provide the environment ID as the value.

1. Choose a combination of [platform and service access roles](/docs/app-configuration?topic=app-configuration-ac-service-access-management) to assign access for the user.

1. Click **Add**.

1. Continue to add platform and service access roles as needed and when you are finished, click **Assign**.

![Access to a specific environment in an instance](images/rbac-inst.png "Access to a specific environment in an instance"){: caption="Figure 2. Access to a specific environment in an instance" caption-side="bottom"}

To enable access to a specific environment in an instance, the user must at least have Reader level privileges to the particular {{site.data.keyword.appconfig_short}} instance.
{: note}
