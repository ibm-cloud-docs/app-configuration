---

copyright:
  years: 2020, [{CURRENT_YEAR}]
lastupdated: "[{LAST_UPDATED_DATE}]"

keywords: app-configuration, app configuration, troubleshooting, faqs, Frequently Asked Questions, question,

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I toggle a newly created feature flag?
{: #ac-troubleshooting-one}
{: troubleshoot}
{: support}

Feature flag is disabled and cannot be toggled.
{: tsSymptoms}

A Feature flag is linked to a collection and the flag is toggled per environment.
{: tsCauses}

If a feature flag is not linked to any collection, it is disabled by default.

Link the feature flag with an existing collection. This allows you to toggle between `ON` or `OFF` state.
{: tsResolve}
