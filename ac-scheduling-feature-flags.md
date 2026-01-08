---

copyright:
  years: 2026
lastupdated: "2026-01-08"

keywords: app-configuration, app configuration, about app configuration, scheduling, feature flags, scheduling feature flags

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Scheduled flags
{: #ac-scheduled-flags}

Scheduling the toggling of feature flags helps users enable or disable a feature of their choice without having to manually toggle the feature flag whenever an event occurs. You can achieve the scheduling of a feature flag with the help of the {{site.data.keyword.en_short}} Periodic Timer. To learn more about the Periodic Timer, see [Periodic Timer](/docs/event-notifications?topic=event-notifications-en-cron-periodic-timer).
{: shortdesc}

## Scheduling a feature flag toggle
{: #ac-scheduling-feature-toggle}

The following steps help a user to schedule the toggle of their feature flags:

1. Create an [{{site.data.keyword.en_short}} instance](/docs/event-notifications?topic=event-notifications-getting-started).

1. Navigate to your {{site.data.keyword.en_short}} instance dashboard and under **Sources**, enable the Periodic Timer source.

1. Create an {{site.data.keyword.appconfig_short}} destination under the **Destinations** tab in the left navigation pane. To learn the process of creating the {{site.data.keyword.appconfig_short}} destination, see [{{site.data.keyword.appconfig_short}}](/docs/event-notifications?topic=event-notifications-en-destination-app-configuration).

1. Create 2 topics with alternating schedules, one to enable the feature flag and another to disable it, with the Periodic timer as the source under the **Topics** tab. To set the cron expression for scheduling, refer to [Periodic Timer](/docs/event-notifications?topic=event-notifications-en-cron-periodic-timer#en-cron-create-topic).

1. Create 2 subscriptions each with one of the topics that were created previously and the {{site.data.keyword.appconfig_short}} destination, under the **Subscriptions** tab. Set one subscription to enable the feature flag and the other to disable the feature flag. You can do this by setting the attribute or [defining a template](/docs/event-notifications?topic=event-notifications-en-app-configuration-notification-template&interface=ui), refer [Configuration](/docs/event-notifications?topic=event-notifications-en-destination-app-configuration#en-appconfig-steps-configure).

Your configuration is now complete. Your feature flag should be enabled and disabled automatically as per the schedule you have defined.
