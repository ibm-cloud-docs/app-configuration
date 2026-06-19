---

copyright:
  years: 2026
lastupdated: "2026-06-18"

keywords: app-configuration, app configuration, rollout strategies, progressive rollout, manual rollout, feature rollout

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Understanding rollout strategies
{: #ac-rollout-strategies}

{{site.data.keyword.appconfig_short}} provides flexible rollout strategies that help you safely release features to your users. Whether you need full control over each release phase or prefer automated, time-based deployments, {{site.data.keyword.appconfig_short}} offers the right approach for your needs.
{: shortdesc}

A rollout strategy determines how a feature flag or property is exposed to your users. By controlling the percentage of users who receive a specific feature variation, you can minimize risk, gather feedback, and ensure stability before a full release.

## Rollout strategy types
{: #ac-rollout-types}

{{site.data.keyword.appconfig_short}} supports two primary rollout strategies: 
* Manual rollout for hands-on control 
* Progressive rollout for automated, time-based deployments. 

Each strategy serves different release management needs and operational preferences.

{{site.data.keyword.appconfig_short}} supports the following rollout strategies:

### Manual rollout
{: #ac-manual-rollout}

Manual rollout provides complete control over feature exposure, allowing you to manually set and adjust the percentage of users who receive a feature at any time.

With manual rollout, you specify a rollout percentage (1-100%) through the {{site.data.keyword.appconfig_short}} dashboard or API. For example, you might start at 10% of users, then manually increase to 25%, 50%, and finally 100% as confidence grows. This approach is ideal when you need full control over each release phase or flexible event-driven schedules. Manual rollout is available in all {{site.data.keyword.appconfig_short}} pricing tiers.

### Progressive rollout
{: #ac-progressive-rollout}

Progressive rollout automates the gradual exposure of features over time, eliminating the need for manual intervention by automatically transitioning between predefined phases according to your schedule.

Progressive rollout is available only for Enterprise tier users.
{: note}

You define multiple phases with specific percentages and durations, and {{site.data.keyword.appconfig_short}} automatically manages the transitions. Choose from predefined templates (1hr, 12hr, 24hr, 48hr) or create custom phases. For example, you might configure a rollout that starts at 5% for 8 hours, increases to 20% for 8 hours, increases to 50% for 8 hours, and completes at 100%. This approach is ideal for automated time-based releases and consistent rollout schedules. Progressive rollout maintains user consistency throughout the rollout and is limited to one progressive rollout per feature flag.

## Comparing rollout strategies
{: #ac-rollout-comparison}

The following table compares the key differences between manual and progressive rollout strategies to help you choose the right approach for your release management needs.

| Feature | Manual rollout | Progressive Rollout |
|---------|---------------|---------------------|
| Automation | Manual | Automated |
| Control level | Full manual control | Scheduled automation |
| Tier availability | All tiers | Enterprise only |
| Rollback | Manual | Manual stop |
| Monitoring integration | External | External |
| Use case | Flexible, event-driven releases | Time-based, predictable releases |
{: caption="Rollout strategy comparison" caption-side="bottom"}

## Choosing the right rollout strategy
{: #ac-choosing-rollout-strategy}

Select the rollout strategy that best aligns with your release management approach, operational requirements, and available tier features.

Choose manual rollout for maximum flexibility, event-driven schedules, or when using Lite, Basic, or Standard tier. Choose progressive rollout for automated time-based releases, consistent schedules, and reduced manual effort (Enterprise tier only).

## Configuring rollout percentage
{: #ac-configure-rollout-percentage}

Rollout percentage controls what portion of your users receive the enabled value of a feature flag, enabling gradual feature exposure and risk mitigation. To configure rollout percentage:

*  Set rollout percentage between 1% and 100%.
* Users are randomly distributed where the specified percentage receives the enabled value and the remaining receives the disabled value.
* Each user's assignment remains consistent across evaluations.
* Configure rollout at the flag level (all users) or rule level (specific targeting rules) to create sophisticated strategies, such as 100% rollout for beta users while maintaining 10% for general users.

## Next steps
{: #ac-rollout-next-steps}

Explore related topics to enhance your feature rollout capabilities and understand the broader context of feature management in {{site.data.keyword.appconfig_short}}.

- [Configure progressive rollout](/docs/app-configuration?topic=app-configuration-ac-progressive-rollout) (Enterprise tier).
- [Target feature flags to segments](/docs/app-configuration?topic=app-configuration-ac-feature-flags#targeting-segment-with-feature-flag).
- [Learn about feature flags](/docs/app-configuration?topic=app-configuration-ac-feature-flags).
- [Understand IAM roles for rollout management](/docs/app-configuration?topic=app-configuration-ac-service-access-management).
