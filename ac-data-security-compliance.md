---

copyright:
  years: 2022
lastupdated: "2022-10-11"

keywords: app-configuration, app configuration, data security, compliance, data security and compliance

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Data security and compliance
{: #ac-data-security-and-compliance}

{{site.data.keyword.appconfig_short}} service has data security strategies in place to meet your compliance needs and ensure that your data remains secure and protected in the cloud.
{: shortdesc}

## Security readiness
{: #ac-security-readiness}

{{site.data.keyword.appconfig_short}} ensures security readiness by adhering to {{site.data.keyword.IBM_notm}} best practices for systems, networking, and secure engineering.

To learn more about security controls across {{site.data.keyword.cloud_notm}}, see [How do I know that my data is safe?](/docs/overview?topic=overview-security#security){: external}.
{: tip}

To learn more about how your data is secured in {{site.data.keyword.appconfig_short}}, see [securing your data in {{site.data.keyword.appconfig_short}}](https://cloud.ibm.com/docs/app-configuration?topic=app-configuration-ac-securing-your-data).

### Data encryption
{: #ac-data-encryption}

Access to {{site.data.keyword.appconfig_short}} takes place over HTTPS and uses Transport Layer Security (TLS) to encrypt data in transit.

For more information on supported TLS ciphers, see [TLS cipher support](/docs/app-configuration?topic=app-configuration-ac-cipher-support).

If you attempt to use a cipher that is not on this list, you may experience connectivity issues. Update your client to use one of the supported ciphers. If you are using `openssl`, you can use the command `openssl ciphers -v` at the command line (or, for some installations of `openssl`, use the `-s -v` options) to show a verbose list of what ciphers your client supports.
{: tip}

## Compliance readiness
{: #ac-compliance-readiness}

{{site.data.keyword.appconfig_short}} meets controls for global, industry, and regional compliance standards, including ISO
27001/27017/27018/27701, and others.

For a complete listing of {{site.data.keyword.cloud_notm}} compliance certifications, see [Compliance on the {{site.data.keyword.cloud_notm}}](https://ibm.com/cloud/compliance){: external}.
{: tip}

### ISO 27001, 27017, 27018, 27701
{: #ac-iso}

{{site.data.keyword.appconfig_short}} is ISO 27001, 27017, 27018, and 27701 certified. You can view compliance certifications by visiting [Compliance on the {{site.data.keyword.cloud_notm}}](https://ibm.com/cloud/compliance){: external}.

## Secrets management
{: #ac-secrets-management}

By integrating {{site.data.keyword.appconfig_short}} with {{site.data.keyword.secrets-manager_short}}, you can store your secrets securely in {{site.data.keyword.secrets-manager_short}} and use the secrets in your application through {{site.data.keyword.appconfig_short}}. {{site.data.keyword.appconfig_short}} stores metadata of {{site.data.keyword.secrets-manager_short}} instance instead of storing the secrets. This metadata is called as a secret reference as part of the **Properties** type in {{site.data.keyword.appconfig_short}}.
