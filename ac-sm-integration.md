---

copyright:
  years: 2022, [{CURRENT_YEAR}]
lastupdated: "[{LAST_UPDATED_DATE}]"

keywords: app-configuration, app configuration, secrets manager, secrets manager integration

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Integrating with {{site.data.keyword.secrets-manager_short}}
{: #ac-sm-integration}

{{site.data.keyword.secrets-manager_full_notm}} helps you to create secrets dynamically and lease them to applications while you control access from a single location. With {{site.data.keyword.secrets-manager_short}}, you can create, lease, and centrally manage secrets that are used in {{site.data.keyword.appconfig_short}} service or your custom-built applications.
{: shortdesc}

By integrating {{site.data.keyword.appconfig_short}} with {{site.data.keyword.secrets-manager_short}}, instead of storing secrets, {{site.data.keyword.appconfig_short}} stores metadata of {{site.data.keyword.secrets-manager_short}} instance. This metadata is called as a secret reference as part of the **Properties** type in {{site.data.keyword.appconfig_short}}.

Take these steps to get {{site.data.keyword.secrets-manager_short}} integrated with {{site.data.keyword.appconfig_short}}:

1. Log in to your {{site.data.keyword.cloud_notm}} account.

1. Create a {{site.data.keyword.secrets-manager_short}} instance and create your secrets.

   If you already have a {{site.data.keyword.secrets-manager_short}} instance, go to next step else create a {{site.data.keyword.secrets-manager_short}} instance. For more information, see [creating a {{site.data.keyword.secrets-manager_short}} instance](https://{DomainName}/docs/secrets-manager?topic=secrets-manager-create-instance&interface=ui).

1. Check the permissions in {{site.data.keyword.secrets-manager_short}} instance.

   Make sure you have a {{site.data.keyword.secrets-manager_short}} instance with *Viewer* access to the resource group where {{site.data.keyword.secrets-manager_short}} instance is created or exists. Also, you need to have *Reader* access to the {{site.data.keyword.secrets-manager_short}} instance.

   For more information about providing user authorizations, see [here](https://{DomainName}/docs/account?topic=account-serviceauth&interface=ui){: external}.

1. Create a property of type *Secret reference*. For more information, see [Properties](/docs/app-configuration?topic=app-configuration-ac-properties).

1. Use the {{site.data.keyword.appconfig_short}} SDKs to connect your application to retrieve and use secrets from {{site.data.keyword.secrets-manager_short}}. For more information on how to access secrets with {{site.data.keyword.appconfig_short}} Node sdk, see [here](/docs/app-configuration?topic=app-configuration-ac-integrate-sdks#ac-integrate-node-evaluate-secret-property).
