---

copyright:
  years: 2020, [{CURRENT_YEAR}]
lastupdated: "[{LAST_UPDATED_DATE}]"

keywords: app-configuration, app configuration, troubleshooting, faqs, Frequently Asked Questions, question,

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Why does deleting a feature flag or property in an environment delete it across all environments?
{: #ac-troubleshooting-del}
{: troubleshoot}
{: support}

Deleting a feature flag or property in an environment deletes it for all environments.
{: tsSymptoms}

Feature flag or property is available to all environments. Updates to values are per environment. Create and delete action executes across all environments.
{: tsCauses}

Deletion of feature flag or property is across all environments.
{: tsResolve}

If a flag is not required in a particular environment, disable the flag or set the values default. If a flag is not required in any environment, it can be deleted.
