---

copyright:
  years: 2021, 2025
lastupdated: "2025-02-06"

keywords: app-configuration, app configuration, managing service access, iam, account, environments

subcollection: app-configuration

content-type: tutorial
account-plan: standard
completion-time: 15m

---

{{site.data.keyword.attribute-definition-list}}

# Assigning access to an individual environment
{: #ac-assign-access-to-environments}
{: toc-content-type="tutorial"}
{: toc-completion-time="15m"}

This tutorial shows you how to assign access roles for Users against Environments, by creating and modifying IAM access policies.
{: shortdesc}

## Before you begin
{: #environment-access-step-0}

If you are already managing instances of App Configuration or IAM, you do not need to create more. However, as this tutorial will modify and configure the instance we are working with, make sure that any accounts or services are not being used in a production environment.

For this tutorial, you need:

- An {{site.data.keyword.cloud}} Platform account
- An instance of {{site.data.keyword.cloud_notm}} {{site.data.keyword.appconfig_short}}
- A Environment to which a user should be constrained
- To complete the steps to manage access to the service, you should be the owner of the {{site.data.keyword.appconfig_short}} instance. In other words, your user ID needs **administrator platform permissions** to use the IAM service. You may have to contact or work with an account administrator.

## Grant Reader access to App Configuration instance
{: #environment-access-step-1}
{: step}

To enable access to a specific environment in an instance, the user must at least have **Reader** level privileges to the particular {{site.data.keyword.appconfig_short}} instance.
{: note}

1. Navigate to IAM by following the **Manage** drop-down menu, and selecting **Access (IAM)**. Follow the **Users** link in the navigation menu, and select the user requiring limited access.
2. Click on **Access** tab. Click on the **Assign access** button. Select the **Access policy** tile and select **App Configuration**.
3. Select the radio toggle next to **Specific resources**. Select **Service Instance** from the _Attribute type_ drop-down menu. Select the {{site.data.keyword.appconfig_short}} instance which you want to assign access. ![Create a new policy](images/tut-iam-env-1.png){: caption="Figure 1: Selecting App Configuration instance."}
4. In the _Roles and access_ section, select the role **Reader**. You'll also need the Platform **Viewer** role, if you don't already have it, in order to view the UI. ![Create a new policy](images/tut-iam-env-2.png){: caption="Figure 2: Selecting Roles for App Configuration instance."}
5. Click **Next** and include conditions if needed which is optional.
6. Click **Add**.

## Grant Manager access to specific Environment
{: #environment-access-step-2}
{: step}

We'll repeat the step 1, but this time we'll use **Environment ID** resource attribute and select **Manager** role.

1. Click on the **Assign access** button. Select the **Access policy** tile and select **App Configuration**.
2. Select the radio toggle next to **Specific resources**. Select **Service Instance** from the _Attribute type_ drop-down menu. Select the {{site.data.keyword.appconfig_short}} instance which you want to assign access.
3. Add another _Attribute type_ by clicking on **Add a condition** button. Select **Environment ID** from the drop-down menu. Type in the ID of the environment that the user should be able to access in the _Value_ field.  In this case, it's a environment called `dev`. ![Create a new policy](images/tut-iam-env-3.png){: caption="Figure 3: Adding resource attribute."}
4. In the _Roles and access_ section, select the role **Manager**. ![Create a new policy](images/tut-iam-env-4.png){: caption="Figure 4: Selecting Roles for resource attribute."}
5. Click **Next** and include conditions if needed which is optional.
6. Click **Add**.

## Review access policies
{: #environment-access-step-3}
{: step}

At this stage, you should have two access policies created as the following image shows. One access policy with **Reader & Viewer**, another with **Manager** role.

![Create a new policy](images/tut-iam-env-5.png){: caption="Figure 5: Review access policies created."}

## Verify that it works
{: #environment-access-step-4}
{: step}

When this {{site.data.keyword.appconfig_short}} instance is accessed by shared user, **Feature flags** & **Properties** are **editable** under the Environment that is given Manager access and **non-editable** under different Environments. ![Create a new policy](images/tut-iam-env-6.png){: caption="Figure 6: Feature flags allowed to edit under environment dev."} ![Create a new policy](images/tut-iam-env-7.png){: caption="Figure 7: Feature flags are view-only or non-editable under environment production."}

When shared user tries to perform any action such as toggle a feature flag, update a feature flag on other environment using API/CLI/Terrform, the action is denied with **401** status code as shown below.
{: note}

```javascript
{
  "status_code": 401,
  "message": "unauthorized: Looks like you do not have access to requested resource or action is not permitted for the corresponding IAM role. If this is a shared resource, please check if access policies are rightly created.",
  "trace": "appconfig-txid-a560b9c5a4dfe218eafbde5419e1651f"
}
```
{: codeblock}

## Next steps
{: #environment-access-next-steps}

Congratulations, you've just set up policies that limit access to a single environment.
