---

copyright:
  years: 2020, 2024
lastupdated: "2024-10-07"

keywords: app-configuration, app configuration, troubleshooting, faqs, Frequently Asked Questions, question,

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Why do I see the values of my feature flags or properties as default values in certain environments?
{: #ac-troubleshooting-def-value}
{: troubleshoot}
{: support}

Default values are assigned to the feature flags or properties in certain environments.
{: tsSymptoms}

A feature flag is always created under an environment.
{: tsCauses}

Though the flag is created under an environment, it is made available to all environments with default values. Flag Values, tags, and segment values are relevant only to the environment where the update is executed.

Feature flag or Property values can be updated specifically to an environment.
{: tsResolve}
