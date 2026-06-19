---

copyright:
  years: 2026
lastupdated: "2026-06-18"

keywords: app-configuration, app configuration, troubleshooting, progressive rollout, inconsistent values, user values

subcollection: app-configuration

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why are users receiving inconsistent values during progressive rollout?
{: #ac-progressive-rollout-ts-inconsistent}
{: troubleshoot}
{: support}

Users are receiving inconsistent values during a progressive rollout.
{: tsSymptoms}

Inconsistent values can occur due to entity ID mismatches, new rollout distributions, or SDK configuration issues.
{: tsCauses}

Verify the following:
{: tsResolve}

1. The same `entity_id` is used for evaluation.
2. Check if a new progressive rollout was started (which generates a new distribution).
3. Ensure the SDK is properly configured and up to date.
