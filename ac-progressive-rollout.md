---

copyright:
  years: 2026
lastupdated: "2026-06-17"

keywords: app-configuration, app configuration, progressive rollout, automated rollout, feature rollout, rollout configuration, rollout constraints

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Configuring progressive rollout
{: #ac-progressive-rollout}

Progressive rollout automates the gradual exposure of feature flags to users over time, eliminating manual intervention and reducing operational effort.

Progressive rollout is available only for Enterprise tier users.
{: important}

## Before you begin
{: #ac-progressive-rollout-prereqs}

Before configuring a progressive rollout, ensure that:
- You have an {{site.data.keyword.appconfig_short}} Enterprise instance
- You have the appropriate IAM permissions (Manager or Writer role)
- You have created a feature flag in your environment

## Progressive rollout overview
{: #ac-progressive-rollout-overview}

Progressive rollout automatically increases feature exposure to users over a scheduled period based on pre-configured time intervals and percentages. You define multiple phases, each with a specific percentage and duration, and {{site.data.keyword.appconfig_short}} automatically manages the transitions between phases.

### Key benefits
{: #ac-progressive-rollout-benefits}

- **Automation**: Eliminates manual intervention for time-based rollouts
- **Consistency**: Ensures the same user receives the same value throughout the rollout
- **Safety**: Allows you to stop the rollout at any phase if issues are detected
- **Flexibility**: Supports custom phase configurations or predefined templates
- **Predictability**: Provides scheduled, time-based feature releases

## Configuration constraints
{: #ac-progressive-rollout-constraints}

Progressive rollout has specific constraints and requirements that you must understand before configuration.

### General constraints
{: #ac-progressive-rollout-general-constraints}

- **Enterprise tier required**: Progressive rollout is available only for Enterprise tier users.
- **One rollout per flag**: Only one progressive rollout is allowed per feature flag. You can configure it at the flag level or at the rule level, but not both at the same time.
- **One active delivery strategy at a time**: If an experiment is running on a flag, you can't create a progressive rollout. Similarly, if a progressive rollout is running, you can't start an experiment on that flag.
- **Percentage range**: Rollout percentage must be between 1% and 100%.

### API requirements by scope
{: #ac-progressive-rollout-config-requirements}

Use the correct API based on where you configure the rollout:

- **Flag-level progressive rollout**: Use the feature flag API to create and update the rollout.
- **Rule-level progressive rollout**: Use the Rules API to create and update the rollout.
- **Stopping a rollout**: Use the stop rollout APIs to stop an active progressive rollout.

### Configuration requirements by scope
{: #ac-progressive-rollout-scope-requirements}

Before you configure a rollout, make sure that the flag or rule uses explicit rollout values:

- **For flag-level progressive rollout**: None of the targeting rules can have a `rolloutPercentage` value inherited from the flag. All targeting rules must use overridden rollout values.
- **For rule-level progressive rollout**: The targeting rule where you add the rollout can't use a value inherited from the flag. The rule must have its own explicit value.

### Blocked operations during progressive rollout
{: #ac-progressive-rollout-blocked-operations}

When a progressive rollout is in the running state, the following operations are blocked:

- **Creating another progressive rollout**: Only one progressive rollout is allowed per flag.
- **Starting an experiment**: Experiments can't run on flags that already have a running progressive rollout.
- **Deleting a collection**: Collection deletion is blocked if any associated feature flag has a progressive rollout in the running state.
- **Updating or deleting a segment**: Segment updates and deletes are blocked if any associated feature flag has a progressive rollout in the running state.
- **Modifying the flag or rule configuration**: Updates to the flag or to the targeting rule that uses the rollout are allowed only when the progressive rollout isn't running.

### Lifecycle behavior
{: #ac-progressive-rollout-lifecycle-behavior}

Keep the following lifecycle behaviors in mind:

- If an experiment is running, you can't create a progressive rollout.
- If a progressive rollout is running, you can't start an experiment on the same flag.
- To stop a rollout, you must use the dedicated stop rollout APIs.

## Configuring a progressive rollout
{: #ac-configure-progressive-rollout}

You can configure progressive rollout at the flag level or at the targeting rule level.

### Configuring flag-level progressive rollout
{: #ac-configure-flag-level-rollout}

To configure progressive rollout at the flag level:

1. In the {{site.data.keyword.appconfig_short}} console, navigate to **Feature flags**.
2. Select the environment containing your feature flag.
3. Click the feature flag you want to configure.
4. In the **Feature rollout** section, select **Progressive** as the rollout type.
5. Configure the rollout settings:
   - **Duration preset**: Choose from predefined templates (1hr, 12hr, 24hr, 48hr) or select **Custom**
   - **Phases**: Define each phase with a percentage and duration
   - **Schedule later** (optional): Toggle this option to specify a start time in UTC for the rollout. If not enabled, the rollout starts immediately.
6. Click **Save**.

The progressive rollout will start automatically at the configured start time.

### Configuring rule-level progressive rollout
{: #ac-configure-rule-level-rollout}

To configure progressive rollout at the targeting rule level:

1. In the {{site.data.keyword.appconfig_short}} console, navigate to **Feature flags**.
2. Select the environment containing your feature flag.
3. Click the feature flag you want to configure.
4. In the **Targeting** section, locate the rule you want to configure.
5. Ensure the rule has an overridden value.
6. In the rule's **Rollout** section, select **Progressive** as the rollout type.
7. Configure the rollout settings:
   - **Duration preset**: Choose from predefined templates (1hr, 12hr, 24hr, 48hr) or select **Custom**
   - **Phases**: Define each phase with a percentage and duration
   - **Schedule later** (optional): Toggle this option to specify a start time in UTC for the rollout. If not enabled, the rollout starts immediately.
8. Click **Save**.

## Progressive rollout phases
{: #ac-progressive-rollout-phases}

A progressive rollout consists of multiple phases, each defining a percentage and duration.

### Phase configuration
{: #ac-progressive-rollout-phase-config}

Each phase includes:
- **Percentage**: The percentage of users who will receive the enabled value (1-100%)
- **Duration**: How long this phase should last (e.g., "8h", "30m", "2d")

The final phase does not require a duration, as it represents the completion state.

### Phase examples
{: #ac-progressive-rollout-phase-examples}

**Example 1: Gradual 24-hour rollout**

```json
{
  "phases": [
    { "percentage": 5, "duration": "6h" },
    { "percentage": 25, "duration": "6h" },
    { "percentage": 50, "duration": "6h" },
    { "percentage": 100, "duration": "6h" }
  ]
}
```

**Example 2: Rapid 1-hour rollout**

```json
{
  "phases": [
    { "percentage": 10, "duration": "15m" },
    { "percentage": 50, "duration": "15m" },
    { "percentage": 100, "duration": "30m" }
  ]
}
```

**Example 3: Conservative 48-hour rollout**

```json
{
  "phases": [
    { "percentage": 5, "duration": "12h" },
    { "percentage": 10, "duration": "12h" },
    { "percentage": 25, "duration": "12h" },
    { "percentage": 100, "duration": "12h" }
  ]
}
```

## Predefined rollout templates
{: #ac-progressive-rollout-templates}

{{site.data.keyword.appconfig_short}} provides predefined templates for common rollout scenarios:

| Template | Duration | Phases |
|----------|----------|--------|
| 1hr | 1 hour | 10% (15m), 50% (15m), 100% (30m) |
| 12hr | 12 hours | 5% (3h), 25% (3h), 50% (3h), 100% (3h) |
| 24hr | 24 hours | 5% (6h), 25% (6h), 50% (6h), 100% (6h) |
| 48hr | 48 hours | 5% (12h), 10% (12h), 25% (12h), 100% (12h) |
{: caption="Predefined rollout templates" caption-side="bottom"}

## Stopping a progressive rollout
{: #ac-stop-progressive-rollout}

You can stop a progressive rollout at any phase if issues are detected.

### Stopping flag-level rollout
{: #ac-stop-flag-rollout}

To stop a flag-level progressive rollout, use the stop rollout API for feature flags.


### Stopping rule-level rollout
{: #ac-stop-rule-rollout}

To stop a rule-level progressive rollout, use the stop rollout API for rules.


### Behavior after stopping
{: #ac-stop-rollout-behavior}

When you stop a progressive rollout:
- The rollout configuration is removed
- The rollout percentage is updated to the specified percentage
- The rollout type reverts to manual rollout
- Users who were receiving the enabled value continue to receive it based on the stopped percentage

## Progressive rollout completion
{: #ac-progressive-rollout-completion}

When a progressive rollout reaches its final phase:
- The rollout configuration is automatically removed
- The rollout percentage is updated to the final phase percentage (typically 100%)
- The rollout type reverts to manual rollout
- All users receive the enabled value

## User consistency and randomization
{: #ac-progressive-rollout-consistency}

Progressive rollout ensures consistent user experience through a two-level randomization strategy:

### Within a rollout
{: #ac-rollout-within-consistency}

During a single progressive rollout:
- Randomization is deterministic per `entity_id`
- The same `entity_id` always receives the same assignment
- Users who receive the enabled value in phase 1 continue to receive it in subsequent phases
- New users are added as the percentage increases

### Across rollouts
{: #ac-rollout-across-consistency}

When you start a new progressive rollout on the same flag:
- A fresh random distribution is generated
- The same `entity_id` may receive a different assignment
- This allows for different user groups to be exposed in different rollout cycles

## Monitoring progressive rollouts
{: #ac-monitor-progressive-rollout}

Monitor your progressive rollouts to ensure they're progressing as expected:

1. **Dashboard view**: The {{site.data.keyword.appconfig_short}} dashboard displays the current status and phase of active progressive rollouts
2. **Status indicators**: 
   - `QUEUED`: Rollout is scheduled but not yet started
   - `RUNNING`: Rollout is actively progressing through phases
3. **Activity tracking**: Use {{site.data.keyword.at_short}} to track rollout events and phase transitions

## Best practices
{: #ac-progressive-rollout-best-practices}

Follow these best practices when configuring progressive rollouts:

- **Start small**: Begin with a low percentage (5-10%) to minimize risk
- **Monitor metrics**: Continuously monitor application metrics during each phase
- **Plan for time zones**: Consider your user base's time zones when scheduling start times
- **Test configurations**: Test your rollout configuration in a non-production environment first
- **Document rollout plans**: Maintain documentation of your rollout strategy and phases
- **Prepare rollback plans**: Have a plan to stop the rollout if issues are detected
- **Use appropriate durations**: Allow sufficient time in each phase to gather meaningful data

## Troubleshooting
{: #ac-progressive-rollout-troubleshooting}

### Cannot configure progressive rollout
{: #ac-progressive-rollout-ts-cannot-configure}

If you cannot configure a progressive rollout, verify:
- You have Enterprise tier access
- No other progressive rollout is active on the flag
- No experiment is running on the flag
- For flag-level rollout: All targeting rules have overridden rollout percentage
- For rule-level rollout: The rule has an overridden value attribute

### Rollout not starting at scheduled time
{: #ac-progressive-rollout-ts-not-starting}

If your rollout doesn't start at the scheduled time:
- Verify the start time is in UTC format
- Ensure the start time is in the future
- Check that the rollout status is `QUEUED`
- Verify your system time is synchronized

### Users receiving inconsistent values
{: #ac-progressive-rollout-ts-inconsistent}

If users are receiving inconsistent values:
- Verify that the same `entity_id` is being used for evaluation
- Check if a new progressive rollout was started (which generates a new distribution)
- Ensure the SDK is properly configured and up to date

## API reference
{: #ac-progressive-rollout-api}

Progressive rollout can be configured using the {{site.data.keyword.appconfig_short}} API. Refer the [API documentation](/apis/app-configuration) for more information.

## Related information
{: #ac-progressive-rollout-related}

- [Understanding rollout strategies](/docs/app-configuration?topic=app-configuration-ac-rollout-strategies)
- [Targeting feature flags to segments](/docs/app-configuration?topic=app-configuration-ac-feature-flags)
- [Managing service access](/docs/app-configuration?topic=app-configuration-ac-service-access-management)
- [{{site.data.keyword.appconfig_short}} API reference](/apis/app-configuration)
