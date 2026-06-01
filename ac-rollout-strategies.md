---

copyright:
  years: 2026
lastupdated: "2026-06-01"

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

{{site.data.keyword.appconfig_short}} supports the following rollout strategies:

### Manual rollout
{: #ac-manual-rollout}

Manual rollout gives you complete control over feature exposure. You manually set and adjust the percentage of users who receive a feature, making changes whenever you choose.

**When to use manual rollout:**
- You need full control over each release phase
- Your release schedule is flexible and event-driven
- You want to manually verify each stage before proceeding
- You're testing features with specific user groups

**How it works:**

With manual rollout, you specify a rollout percentage (1-100%) that determines what portion of your users receive the enabled value of a feature flag. The remaining users receive the disabled value. You can adjust this percentage at any time through the {{site.data.keyword.appconfig_short}} dashboard or API.

For example, you might start by exposing a new feature to 10% of users, monitor the results, then manually increase to 25%, 50%, and finally 100% as confidence grows.

**Key characteristics:**
- Requires manual intervention to change rollout percentages
- Provides maximum flexibility and control
- Available in all {{site.data.keyword.appconfig_short}} pricing tiers
- Can be configured at the flag level or within specific targeting rules

### Progressive rollout
{: #ac-progressive-rollout}

Progressive rollout automates the gradual exposure of features over time. You define multiple phases with specific percentages and durations, and {{site.data.keyword.appconfig_short}} automatically transitions between phases according to your schedule.

Progressive rollout is available only for Enterprise tier users.
{: note}

**When to use progressive rollout:**
- You want to automate time-based feature releases
- You need consistent, predictable rollout schedules
- You want to reduce manual operational effort
- You're releasing features across multiple time zones or regions

**How it works:**

You configure a progressive rollout by defining:
- **Duration preset**: Choose from predefined templates (1hr, 12hr, 24hr, 48hr) or create custom phases
- **Phases**: Multiple stages, each with a percentage and duration
- **Schedule later** (optional): Toggle this option to specify a start time in UTC for the rollout. If not enabled, the rollout starts immediately.

For example, you might configure a progressive rollout that:
1. Starts at 5% for 8 hours
2. Increases to 20% for 8 hours
3. Increases to 50% for 8 hours
4. Completes at 100%

{{site.data.keyword.appconfig_short}} automatically manages the transitions between phases, eliminating the need for manual intervention.

**Key characteristics:**
- Automates rollout progression based on time intervals
- Supports custom phase configurations or predefined templates
- Can be stopped at any phase if issues are detected
- Maintains user consistency throughout the rollout
- Available only in Enterprise tier
- Limited to one progressive rollout per feature flag

**User consistency:**

Progressive rollout ensures that the same user consistently receives the same value during a rollout. This is achieved through a two-level randomization strategy:
1. **Within a rollout**: The same user always receives the same assignment
2. **Across rollouts**: Each new progressive rollout generates a fresh distribution

## Comparing rollout strategies
{: #ac-rollout-comparison}

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

Consider these factors when selecting a rollout strategy:

**Choose manual rollout if:**
- You need maximum flexibility and control
- Your release schedule is event-driven rather than time-based
- You want to manually verify each stage before proceeding
- You're using Lite, Basic, or Standard tier

**Choose progressive rollout if:**
- You want to automate time-based releases
- You need consistent, predictable rollout schedules
- You want to reduce manual operational effort
- You have Enterprise tier access
- You're comfortable with scheduled, automated transitions

## Configuring rollout percentage
{: #ac-configure-rollout-percentage}

Rollout percentage determines what portion of your users receive the enabled value of a feature flag. The percentage can be set between 1% and 100%.

**How manual rollout works:**

When you set a rollout percentage:
- Users are randomly distributed into groups
- The specified percentage receives the enabled value
- The remaining percentage receives the disabled value
- The same user consistently receives the same value (deterministic assignment)

For example, with a 30% rollout:
- 30% of users receive the enabled value
- 70% of users receive the disabled value
- Each user's assignment remains consistent across evaluations

**Rollout scope:**

Rollout percentage can be configured at two levels:
1. **Flag level**: Applies to all users who don't match any targeting rules
2. **Rule level**: Applies only to users who match specific targeting rules

This flexibility allows you to create sophisticated rollout strategies, such as rolling out to 100% of beta users while maintaining 10% rollout for general users.

## Next steps
{: #ac-rollout-next-steps}

- [Configure progressive rollout](/docs/app-configuration?topic=app-configuration-ac-progressive-rollout) (Enterprise tier)
- [Target feature flags to segments](/docs/app-configuration?topic=app-configuration-ac-feature-flags#targeting-segment-with-feature-flag)
- [Learn about feature flags](/docs/app-configuration?topic=app-configuration-ac-feature-flags)
- [Understand IAM roles for rollout management](/docs/app-configuration?topic=app-configuration-ac-service-access-management)
