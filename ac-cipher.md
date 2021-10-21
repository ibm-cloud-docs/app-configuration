---

copyright:
  years: 2021
lastupdated: "2021-10-21"

keywords: app-configuration, app configuration, securing your data

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

# TLS cipher support
{: #ac-cipher-support}

{{site.data.keyword.appconfig_short}} API endpoints supports only TLS version >= 1.2.  Additionally {{site.data.keyword.appconfig_short}} API end points will allow only the following cipher suites:
{: shortdesc}

- `ECDHE-ECDSA-AES128-GCM-SHA256`
- `ECDHE-ECDSA-CHACHA20-POLY1305`
- `ECDHE-ECDSA-AES256-GCM-SHA384`
- `ECDHE-RSA-AES128-GCM-SHA256`
- `ECDHE-RSA-CHACHA20-POLY1305`
- `ECDHE-RSA-AES256-GCM-SHA384`


