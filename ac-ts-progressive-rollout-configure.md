---

copyright:
  years: 2026
lastupdated: "2026-06-18"

keywords: app-configuration, app configuration, troubleshooting, progressive rollout, cannot configure, configuration failed

subcollection: app-configuration

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I configure progressive rollout?
{: #ac-progressive-rollout-ts-cannot-configure}
{: troubleshoot}
{: support}

You are unable to configure a progressive rollout for your feature flag.
{: tsSymptoms}

Progressive rollout configuration may fail due to tier restrictions, conflicting configurations, or missing prerequisites.
{: tsCauses}

Verify the following requirements:
{: tsResolve}

1. You have Enterprise tier access.
2. No other progressive rollout is active on the flag.
3. No experiment is running on the flag.
4. For flag-level rollout: All targeting rules have overridden rollout percentage.
5. For rule-level rollout: The rule has an overridden value attribute.
