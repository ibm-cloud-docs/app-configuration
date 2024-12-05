---

copyright:
  years: 2020, 2024
lastupdated: "2024-10-07"

keywords: app-configuration, app configuration, troubleshooting, faqs, Frequently Asked Questions, question, rate limiting

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Why am I receiving the "429 Too Many Requests" status code as a response to API calls?
{: #ac-troubleshooting-rate-limiting}
{: troubleshoot}
{: support}

API requests to {{site.data.keyword.appconfig_short}} service is returning the HTTP status code as 429.
{: tsSymptoms}

All the APIs of the {{site.data.keyword.appconfig_short}} service are rate-limited. Excessive number of requests sent to {{site.data.keyword.appconfig_short}} from a single source will be blocked if they exceed the threshold value within a specific time period.
{: tsCauses}

Evaluate the reason of the excessive requests being sent to {{site.data.keyword.appconfig_short}} exceeding the threshold value. Also, you may retry the request again after the interval specified in the `retry-after` response header.
{: tsResolve}
