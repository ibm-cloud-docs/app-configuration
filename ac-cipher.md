---

copyright:
  years: 2021, 2022
lastupdated: "2022-10-11"

keywords: app-configuration, app configuration, securing your data

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# TLS cipher support
{: #ac-cipher-support}

{{site.data.keyword.appconfig_short}} API endpoints support only TLS version >= 1.2. Additionally {{site.data.keyword.appconfig_short}} API end points allows only the following cipher suites:
{: shortdesc}

- `ECDHE-ECDSA-AES128-GCM-SHA256`
- `ECDHE-ECDSA-CHACHA20-POLY1305`
- `ECDHE-ECDSA-AES256-GCM-SHA384`
- `ECDHE-RSA-AES128-GCM-SHA256`
- `ECDHE-RSA-CHACHA20-POLY1305`
- `ECDHE-RSA-AES256-GCM-SHA384`
