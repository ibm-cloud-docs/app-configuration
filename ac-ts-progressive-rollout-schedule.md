---

copyright:
  years: 2026
lastupdated: "2026-06-18"

keywords: app-configuration, app configuration, troubleshooting, progressive rollout, scheduled time, rollout not starting

subcollection: app-configuration

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my rollout not starting at the scheduled time?
{: #ac-progressive-rollout-ts-not-starting}
{: troubleshoot}
{: support}

Your progressive rollout doesn't start at the scheduled time.
{: tsSymptoms}

Scheduling issues can occur due to incorrect time format, past start times, or system time synchronization problems.
{: tsCauses}

Verify the following:
{: tsResolve}

1. The start time is in UTC format.
2. The start time is in the future.
3. The rollout status is `QUEUED`.
4. Your system time is synchronized.
