---

copyright:
  years: 2022
lastupdated: "2022-12-06"

keywords: app-configuration, app configuration, troubleshooting, faqs, Frequently Asked Questions, question, rate limiting

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
{:java: .ph data-hd-programlang='java'}
{:ruby: .ph data-hd-programlang='ruby'}
{:c#: .ph data-hd-programlang='c#'}
{:objectc: .ph data-hd-programlang='Objective C'}
{:python: .ph data-hd-programlang='python'}
{:javascript: .ph data-hd-programlang='javascript'}
{:php: .ph data-hd-programlang='PHP'}
{:swift: .ph data-hd-programlang='swift'}
{:reactnative: .ph data-hd-programlang='React Native'}
{:csharp: .ph data-hd-programlang='csharp'}
{:ios: .ph data-hd-programlang='iOS'}
{:android: .ph data-hd-programlang='Android'}
{:cordova: .ph data-hd-programlang='Cordova'}
{:xml: .ph data-hd-programlang='xml'}
{:new_window: target="_blank"}
{:table: .aria-labeledby="caption"}
{:deprecated: .deprecated}
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:term: .term}
{:troubleshoot: data-hd-content-type='troubleshoot'}

# Why am I receiving the Status Code - "429 Too Many Requests" as response to the API Calls?
{: #ac-troubleshooting-rate-limiting}
{: troubleshoot}
{: support}

API requests to {{site.data.keyword.appconfig_short}} service is returning the HTTP status code as 429.
{: tsSymptoms}

All the APIs of the {{site.data.keyword.appconfig_short}} service are rate-limited. Excessive number of requests sent to {{site.data.keyword.appconfig_short}} from a single source will be blocked if they exceed the threshold value within a specific time period.
{: tsCauses}

Evaluate the reason of the excessive requests being sent to {{site.data.keyword.appconfig_short}} exceeding the threshold value. Also, you may retry the request again after the interval specified in the `retry-after` response header.
{: tsResolve}
