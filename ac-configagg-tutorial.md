---

copyright:
   years: 2024
lastupdated: "2024-11-26"

keywords: app-configuration, app configuration,enable configuration aggregation,tutorial

subcollection: app-configuration

content-type: tutorial
account-plan: standard
completion-time: 40m

---

{{site.data.keyword.attribute-definition-list}}

# Working with Configuration Aggregator as a support for Enterprise Accounts
{: #ac-caea-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="40m"}

This tutorial shows how the [Configuration Aggregator](/docs/app-configuration?topic=app-configuration-ac-configuration-aggregator) feature can be configured on an {{site.data.keyword.appconfig_short}} instance at Enterprise account level to collect resource metadata from all the sub-accounts of the enterprise.
{: shortdesc}

## Before you begin
{: #ac-prereqs-ca}

Ensure that the following prerequisites are in place:

* Create an {{site.data.keyword.appconfig_short}} instance at the top-level of the enterprise i.e enterprise account.
* Create a Trusted Profile Template providing access for the App Configuration service instance to the IAM enabled services and Account Management services. See section below on the Steps to create the Trusted profile template.
* Assign the Trusted profile template to the required accounts and account groups in the Enterprise. This will create the trusted properties in all the selected accounts.
* App Configuration needs access to read the trusted profile templates. Create a trusted profile with access for Template Administrator, Assignment Administrator, viewer on All IAM Account Management services.
   <img width="1713" alt="Screenshot 2024-05-26 at 9 25 08 AM" src="https://media.github.ibm.com/user/885/files/c1c34b7c-e883-48c9-b10a-a47c8fc111da">

The Enterprise IAM should be enabled in the sub-accounts of an Enterprise to be managed via Enterprise. Ensure that this option is enabled, or you can modify it using the below API.

```curl
curl -s -L -X PATCH "https://accounts.test.cloud.ibm.com/v1/accounts/$ACCOUNT/traits" 
-H "Content-Type: application/json" 
-H "Authorization: Bearer $TOKEN" 
-d "{
    \"enterprise_iam_managed\": true
}"
```
{: codeblock}
{: note}

If the trusted profile template is applied to an account group, then all the accounts and account group added in the future will also get assigned to the trusted profile template automatically.
{: note}

## Steps for Creating a Trusted Profile Template

  **Step 1: Create a trusted profile template that can be used to apply to all the child accounts in the Enterprise account**
   
   The configuration for the template looks like below. The steps below guide you on how to create it. 
   
   <img width="1721" alt="Screenshot 2024-05-26 at 9 16 06 AM" src="https://media.github.ibm.com/user/885/files/3a87d9b7-0e45-4805-a2a0-82c5e6bb39a3">
    
   *Trusted Profile template configured and committed*
   
   <img width="1685" alt="Screenshot 2024-05-26 at 9 16 37 AM" src="https://media.github.ibm.com/user/885/files/ea2cbd59-833a-4d5e-82c7-c8f67d35f846">
   
   *Assigned access policies*
   
   <img width="1680" alt="Screenshot 2024-05-26 at 9 17 02 AM" src="https://media.github.ibm.com/user/885/files/fef279b6-9d93-4e19-8c00-da1a9e10be84">
   
   *Accounts assignments*

   **Step 2: Create policy templates** 
   
   Create template policies so that it can be used in a TP template. For the Configuration Aggregator functionality, the trusted policy would need access to `All IAM enabled services` with `Reader, Viewer and ConfigReader` roles & `All Account Management services` with `Viewer and Config Reader` role. 
   
   The policy template can be created using API only. Refer - API: https://cloud.ibm.com/docs/secure-enterprise?topic=secure-enterprise-policy-template-create&interface=api 
   
   Payload for creating the policy templates 
   
   **Policy template 1 : IAM Enabled services**
   ```
   POST https://iam.test.cloud.ibm.com/v1/policy_templates 
   ```
   
   ```json
   {
     "name": "All IAM enabled services",
     "description": "Reader Access for all the IAM enabled services",
     "account_id": "c1d20fee2fe24c42b8ef6583283d2dcf",
     "policy": {
        "type": "access",
        "description": "Reader Access for all the IAM enabled services",
        "control": {
           "grant": {
           "roles": [
             {
                  "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Reader"
               },
               {
                  "role_id": "crn:v1:bluemix:public:iam::::role:Viewer"
               },
               {
                  "role_id": "crn:v1:bluemix:public:iam::::role:ConfigReader"
               }
           ]
         }
       },
       "resource": 
         {
           "attributes": [
               {
                  "key": "serviceType",
               "operator": "stringEquals",
               "value": "service"
               }
           ]
         }

     }
   }
   ```
   
   **Policy Template 2: Account Management services**
   
   ```
   POST https://iam.test.cloud.ibm.com/v1/policy_templates
   ```
   
   ```json
   {
     "name": "Account Management Services",
     "description": "Reader Access for all Account Management Services",
     "account_id": "c1d20fee2fe24c42b8ef6583283d2dcf",
     "policy": {
        "type": "access",
        "description": "Reader Access for all Account Management Services",
        "control": {
           "grant": {
           "roles": [
               {
                  "role_id": "crn:v1:bluemix:public:iam::::role:Viewer"
               },
               {
                  "role_id": "crn:v1:bluemix:public:iam::::role:ConfigReader"
               }
           ]
         }
       },
       "resource": 
         {
           "attributes": [
               {
                  "key": "serviceType",
               "operator": "stringEquals",
               "value": "platform_service"
               }
           ]
         }

     }
   }
   ```
   
   The policy templates created are as below : 
   
   <img width="1451" alt="Screenshot 2024-05-26 at 9 38 03 AM" src="https://media.github.ibm.com/user/885/files/3d554d65-6575-4e14-9a58-c874e2a71807">

---
   **Step 3: Create Trusted Profile Template with IBM Cloud service instance as a trusted identity**
   
   In order to create a TP template with IBM Cloud service instance as a trusted identity, you need to use the APIs. Also ensure to use `type: crn` for the identities. Refer for more details : https://cloud.ibm.com/docs/secure-enterprise?topic=secure-enterprise-tp-template-create&interface=api#create-trusted-profile-template-api.
   
   **Payload for creating trusted profile template:** 
   
   ```
   POST https://iam.test.cloud.ibm.com/v1/profile_templates
   ```
   
   ```json
   {
     "account_id": "c1d20fee2fe24c42b8ef6583283d2dcf",
     "name": "Configuration Aggregator Template", 
     "description": "Trusted profile template for Config Aggregator to collect resources from services",
      "profile": {
           "name": "Configuration Aggregator",
           "description": "Trusted Profile to collect resources via Config Aggregator",
           "identities": [
             {
               "type": "crn",
               "identifier": "crn:v1:staging:public:apprapp-dev:us-south:a/c1d20fee2fe24c42b8ef6583283d2dcf:8abc9e31-5e7e-4154-b2d1-e963ee8a85a2::",
               "description": "App Configuration Dev instance in Enterprise account"
             }
           ]
       },
       "policy_template_references": [
         {
           "id": "policyTemplate-1362f690-8e7f-4a0a-bf72-bb8e5a0008c5",
           "version": "1"
         },
         {
           "id": "policyTemplate-2ba51f58-7b02-47ba-a707-1916d4650cbf",
           "version": "1"
         }
       ]
   }
   ```
   `identities.identifier` refers to the App Configuration instance CRN that is being configured for Configuration Aggregator. 
   `policy_template_references.id` refers to the id of the policy templates created in previous step. 
   
Once the template is created it will show up in draft mode.
   
---
   
   **Step 4: Commit the template**
   
   Once we have all the details such as policy and identities in place then you can make an update and mark it as committed using https://cloud.ibm.com/docs/secure-enterprise?topic=secure-enterprise-tp-template-create&interface=api#update-trusted-profile-template-api


   ```
   POST https://iam.test.cloud.ibm.com/v1/profile_templates/{{template_id_from_previous__step}}/versions/1/commit
   ```
   
   No payload body is required
   {: note}

   
   **Step 5: Assign accounts to the templates**
   
   Once the template is committed, it can be used for assignments. You can use the UI or API for this. You can do assignments only to the accounts that have `enterprise_iam_managed` enabled. 
   
   - API: https://cloud.ibm.com/docs/secure-enterprise?topic=secure-enterprise-tp-template-create&interface=api#assign-trusted-profile-template-api
   - UI: https://cloud.ibm.com/docs/secure-enterprise?topic=secure-enterprise-tp-template-create&interface=ui#assign-trusted-profile-template-api
   
   <img width="1562" alt="Screenshot 2024-05-26 at 8 18 07 PM" src="https://media.github.ibm.com/user/885/files/d7e5d592-bb0e-4c63-bbfc-101c611fdc62">
   
   
   <img width="1451" alt="Screenshot 2024-05-26 at 8 32 33 PM" src="https://media.github.ibm.com/user/885/files/fb250041-b707-4ec4-967b-ca70eb9e1a6c">

   Once the assignment is complete, the trusted profile will be created in all the sub-accounts. It can be validated by checking the accounts that shows that the trusted profile is enterprise-managed.
   
   <img width="1439" alt="Screenshot 2024-05-26 at 8 34 18 PM" src="https://media.github.ibm.com/user/885/files/cd06178c-012a-4c23-8497-197a30dfe6ea">
   
   
</details>

#### Steps to configure App Configuration for an Enterprise account

   **Step 1: Create a trusted profile template**
   Create a trusted profile template as mentioned in the above section and assign it to all the required sub-accounts.

   **Step 2:Collecting Resource Metadata**
   If you choose to collect resource metadata of the top-level enterprise account, then a separate trusted file should be created in the enterprise account. 

   The trusted profile template cannot be assigned to an enterprise account.
   {: note}

   **Step 3: Create Trusted Profile template to provide access to App Configuration service instance access**
   Create a trusted profile that provides the App Configuration service instance access to get the list of TP assignments of the profile template. The trusted profile configuration should be as shown below. This will be used by the service to fetch the trusted profile id and generate authorization required to fetch resource metadata from the accounts selected in the Enterprise.  

   <img width="1469" alt="Screenshot 2024-05-26 at 11 45 30 PM" src="https://media.github.ibm.com/user/885/files/597a9f64-0328-4ae5-a8e4-b2984eaceae1">

   **Step 4: Configure the Configuration Aggregator**
   Configure the Configuration aggregator using the [Settings API](/apidocs/app-configuration#replace-settings). See the API documentation for more details. 


#### Resource collection for an Enterprise account
- When an Enterprise is configured for resource collection, the config manager will fetch the resources from each of the configured accounts during the reconciliation process. 
- During the reconciliation, the config manager retrieves the template assignments for the template. Using the template assignment API, retrieve the list of accounts and the corresponding trusted profile ID for the account. 
- It fetches the resources for each of the configured accounts using the trusted profile token generated from the trusted profile obtained from the template assignment APIs. See [here](https://github.ibm.com/devx-app-services/architecture/blob/development/tri_docs/config-aggregator/aggregator.md#steps-for-fetching-account-and-trusted-profile-details-for-a-enterprise-account) for the details on how to fetch the trusted profile details from the template assignments. 
- Also, during reconciliation, the Config Manager calls the Hyperwarp Listener to ensure that the required accounts are registered with Hyperwarp for the resource lifecycle events. 
- For each deep config of resources stored for an account in an Enterprise, the enterprise ID is also added as part of the resource metadata. 
- The Query API should allow querying by a filter of account_id for an Enterprise. The filter will not be allowed for a normal account. 
