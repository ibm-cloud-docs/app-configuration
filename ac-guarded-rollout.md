---

copyright:
  years: 2026
lastupdated: "2026-09-30"

keywords: app-configuration, app configuration, guarded rollout, automated rollback, metric guardrail, feature rollout, safe deployment

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Configuring guarded rollout
{: #ac-guarded-rollout}

Guarded rollout automates the gradual exposure of feature flags to users over time, and adds an intelligent fail-safe mechanism that continuously monitors deployment health through configurable metric guardrails. If any monitored metric shows a credible regression, {{site.data.keyword.appconfig_short}} rolls back the rollout to 0% automatically if you have enabled the **Auto rollback** toggle, or pauses the rollout and notifies you if you have not.
{: shortdesc}

Guarded rollout is available only for Enterprise tier users.
{: important}

## Benefits of guarded rollout
{: #ac-benefits-guarded-rollout}

- **Automated protection**: Metric guardrails continuously monitor deployment health and trigger rollback without manual intervention.
- **Accurate regression detection**: Statistical analysis compares the new variation against the original to detect credible negative impacts before they affect all users.
- **Flexible configuration**: Define custom rollout phases or use predefined templates, with multiple metrics per guardrail.
- **Pause and resume**: When **Auto rollback** is not enabled, a detected regression pauses the rollout and notifies you for manual review instead of stopping automatically.
- **Audit trail**: Phase transitions, metric evaluations, and rollback events are preserved for historical review.

## Before you begin
{: #ac-guarded-rollout-prereqs}

Before configuring guarded rollout, ensure that:

- You have an {{site.data.keyword.appconfig_short}} Enterprise instance.
- You have the appropriate IAM permissions (Manager or Writer role).
- You have created a feature flag in your environment.
- No experiment is currently running on the feature flag you want to configure.

## How guarded rollout works
{: #ac-guarded-rollout-overview}

A guarded rollout delivers a specific flag variation to a defined percentage of users (`entity_id`s) and gradually increases that percentage over time. During each rollout phase, {{site.data.keyword.appconfig_short}} continuously evaluates the configured metric guardrails to compare the new variation against the original (control) variation.

The rollout uses a two-variation split within the guarded percentage: both the new and original variations each receive the same share of guarded traffic for a statistically valid comparison. For example, at a 10% rollout phase, 10% of users receive the new variation and 10% receive the original variation as control. The remaining 80% of users receive the original variation outside the guarded analysis.

The maximum rollout percentage for a guarded rollout phase is 50%.
{: note}

At each evaluation checkpoint, {{site.data.keyword.appconfig_short}} determines one of the following outcomes:

- **No regression detected**: The rollout continues to the next phase as scheduled.
- **Regression detected, Auto rollback enabled**: The rollout automatically reverts to 0%, a notification is sent, and the rollout type changes to manual. The rollout status is set to `ROLLED_BACK`.
- **Regression detected, Auto rollback not enabled**: The rollout is paused at the current percentage. You receive a notification and must manually choose to continue or stop the rollout. The rollout status is set to `PAUSED`.
- **Insufficient data at end of rollout**: The last stage is extended by an equal duration. If data remains insufficient after the extension, the rollout rolls back to 0% and a notification is sent. The rollout status is set to `ROLLED_BACK`.
- **Inconclusive at end of final stage**: The rollout completes to 100%, because no regression was detected. The rollout status is set to `COMPLETED`.

When all phases complete successfully, {{site.data.keyword.appconfig_short}} removes the guarded rollout configuration, updates the rollout percentage to 100%, and changes the rollout type to manual.

The following rollout statuses are used throughout the lifecycle:

| Status | Meaning |
|--------|---------|
| `IN_PROGRESS` | The rollout is actively progressing through its stages. |
| `PAUSED` | The rollout has been paused due to a detected regression (when **Auto rollback** is not enabled) or because it is awaiting more data. |
| `STOPPED` | The rollout was manually stopped before completion. |
| `COMPLETED` | All stages completed successfully. The rollout percentage is set to 100% and the rollout type reverts to manual. |
| `ROLLED_BACK` | The rollout was reverted to 0%, either automatically due to a detected regression or insufficient data. |
{: caption="Guarded rollout statuses" caption-side="bottom"}

## Configuration constraints
{: #ac-guarded-rollout-constraints}

Review all constraints before configuring a guarded rollout.

- **Enterprise tier required**: Guarded rollout is available only for Enterprise tier users.
- **One rollout per flag**: Only one guarded or progressive rollout is allowed per feature flag at a time.
- **No concurrent experiment**: Guarded rollout cannot be configured if an experiment is running on the flag. Similarly, you cannot start an experiment on a flag that has a running guarded rollout.
- **Maximum rollout percentage**: The maximum rollout percentage per phase is 50%, to ensure equal distribution between the new and original variations.
- **Increasing phase percentages**: Each phase's rollout percentage must be greater than the previous phase's percentage.
- **Minimum start time**: If scheduling a start time, it must be at least 10 minutes from the current time.
- **Flag-level scope**: All targeting rules must use overridden rollout percentage values. No targeting rule can inherit the rollout percentage from the flag level.
- **Rule-level scope**: The targeting rule where you add the guarded rollout must use an overridden value attribute. The rule cannot inherit the value from the flag.

When a guarded rollout is running, the following operations are blocked:

- Creating another guarded or progressive rollout on the same flag.
- Starting an experiment on the flag.
- Deleting a collection associated with the flag.
- Updating or deleting a segment associated with the flag.
- Modifying the flag or targeting rule configuration while the rollout is running.

## Metric guardrails
{: #ac-guarded-rollout-metrics}

Metric guardrails define the health criteria that must be satisfied for the rollout to continue. You can configure multiple metric guardrails per guarded rollout. All guardrails must pass for the rollout to proceed to the next phase.

When you create a metric, you specify an **event key** that connects your application code to the metric definition in {{site.data.keyword.appconfig_short}}. When the event occurs in your application, your code calls `track()` with that event key. {{site.data.keyword.appconfig_short}} matches the incoming event to all metrics configured with that key and attributes it to the correct variation group for analysis. The event key in your metric and the event key in your application code must match exactly. A mismatch means the event is never attributed to the metric, and the guardrail receives no data. The event key is not required to be unique — multiple metrics can share the same event key.

Two measurement types are supported:

| Measurement type | Description | Calculation |
|------------------|-------------|-------------|
| **Occurrence** | Tracks whether an event occurred at least once. A simple yes/no per user session. Use this when the presence of the event itself is the signal. | Measures the percentage of users who triggered the event at least once. |
| **Count** | Tracks the total number of times an event occurs. Use this when the volume of events matters, not just whether it happened. | Measures the average number of times the event occurred per user. |
{: caption="Supported metric measurement types" caption-side="bottom"}

{{site.data.keyword.appconfig_short}} compares the performance of the new variation against the original (control) variation to determine whether a regression has occurred. Each metric specifies whether higher or lower values are better, which determines what counts as a negative impact:

- **Higher-is-better metrics** (for example, conversion rate): A regression is detected when the new variation's value is significantly lower than the original variation's value.
- **Lower-is-better metrics** (for example, error rate, latency): A regression is detected when the new variation's value is significantly higher than the original variation's value.
- **Inconclusive**: If the analysis cannot confirm a negative impact, no regression is detected and the rollout continues.

The following minimum sample sizes per variation are required before a decision is made:

| Metric type | Minimum sample size per variation |
|-------------|-----------------------------------|
| OCCURRENCES (binary) | 100 entities |
| COUNTS | 250 entities |
{: caption="Minimum sample sizes for metric evaluation" caption-side="bottom"}

The last stage is automatically extended by an equal duration in the following situations:

- No sufficient data or no metric events have been received by the end of the stage.
- The rollout is in a paused state at the end of the last-minus-one stage.

If the sample size is still insufficient after the extension, the rollout rolls back to 0% and a notification is sent.

Each metric is evaluated and assigned one of the following statuses:

| Metric status | Meaning |
|---------------|---------|
| `NO_EVENTS` | No metric events have been received for this metric. |
| `INSUFFICIENT_DATA` | Events are being received but the sample size is not yet large enough to evaluate the metric reliably. |
| `INCONCLUSIVE_HEALTHY` | The result is inconclusive with no indication of harm. The rollout is considered safe and continues. |
| `INCONCLUSIVE_WORSE` | The result is inconclusive but the metric is trending in a worse direction. The rollout continues but may be flagged as a warning. |
| `HEALTHY` | The metric shows no negative impact. The rollout is safe to continue. |
| `REGRESSED` | A statistically significant negative impact has been detected. The rollout is paused or rolled back depending on your **Auto rollback** setting. |
{: caption="Metric evaluation statuses" caption-side="bottom"}

## Paused rollout behavior
{: #ac-guarded-rollout-paused}

When **Auto rollback** is not enabled and a regression is detected, the rollout enters a paused state. The pause lifecycle has the following statuses:

| Status | Meaning |
|--------|---------|
| `PAUSE_AUTO` | Regression detected. Rollout paused automatically at the current percentage. |
| `PAUSE_SAMPLE_COLLECTION` | You chose to proceed after a pause. Rollout is waiting for the minimum number of new samples before re-evaluating. |
| `PAUSE_CONTINUE` | Minimum new sample size reached. Evaluation is in progress. |
| `PAUSE_FINAL_STAGE` | End of the last-minus-one stage reached with a regression that has improved compared to the previous paused regression value. You must choose to either roll back to 0% or complete to 100%. |
{: caption="Pause lifecycle statuses for guarded rollout" caption-side="bottom"}

After you choose to proceed from a `PAUSE_AUTO` state, the rollout does not re-evaluate until the minimum number of new samples has been collected. The rollout pauses again only if the absolute difference of the metric has worsened compared to the value at the previous regression. At the end of the last-minus-one stage, if the metric has worsened, the rollout automatically rolls back to 0%. If it has improved, you are prompted to choose rollback to 0% or completion to 100%.

## Creating a metric
{: #ac-guarded-rollout-create-metric}

Metrics measure the impact of your feature flag on user behavior or system performance. You must create at least one metric before you can configure metric guardrails for a guarded rollout.

To create a metric:

1. In the {{site.data.keyword.appconfig_short}} console, select **Metrics** from the left navigation pane.
2. Click **Create Metric**.
3. Provide a name and event key. Optionally add a description.

   The event key identifies the user action or system event to track. The event key in your metric and the event key in your application code must match exactly. The event key can have a maximum of 100 characters.
   {: note}

4. Select a **Measurement type**:
   - **Occurrence**: Tracks whether an event occurred at least once per user session (binary). Use this when the presence of the event is the signal.
   - **Count**: Tracks the total number of times an event occurs. Use this when the volume of events matters.
5. Select a **Direction**:
   - **Higher is better**: The rollout is healthy when values go up. For example, more checkouts or higher usage.
   - **Lower is better**: The rollout is healthy when values go down. For example, fewer errors or lower latency.

6. Click **Save**.

   If the metric is currently used in an active guarded rollout, certain fields cannot be edited to avoid impacting the running rollout.
   {: note}

You can mark a metric as a favourite from the actions menu ![Overflow menu](/images/overflow-menu.svg). Favourited metrics appear at the top of the list when selecting guardrails for a guarded rollout.

## Configuring guarded rollout
{: #ac-configure-guarded-rollout}

You can configure guarded rollout at the flag level or at the targeting rule level. Before you begin, [create the metrics](#ac-guarded-rollout-create-metric) you want to use as guardrails.

### Configuring flag-level guarded rollout
{: #ac-configure-flag-level-guarded-rollout}

To configure guarded rollout at the flag level:

1. In the {{site.data.keyword.appconfig_short}} console, navigate to **Feature flags**.
2. Select the environment containing your feature flag.
3. Click the feature flag you want to configure.
4. In the **Feature rollout** section, select **Guarded** as the rollout type.
5. Select a **Duration preset** from the predefined templates (1hr, 12hr, 24hr, 48hr) or select **Custom**.
6. Define each phase with a rollout percentage (maximum 50%) and a duration. Each phase's percentage must be greater than the previous phase's percentage.
7. Add one or more metrics to monitor as guardrails. Select a metric from the list and click **Add+**. Repeat for each additional metric. To create a new metric, see [Creating a metric](#ac-guarded-rollout-create-metric).
8. Toggle **Auto rollback** to enable automatic revert to 0% if a regression is detected. If not enabled, a regression pauses the rollout and notifies you instead.
9. (Optional) Toggle **Schedule later** to specify a start time in UTC. The scheduled start time must be at least 10 minutes from the current time. If not enabled, the rollout starts immediately.
10. Click **Save**.

### Configuring rule-level guarded rollout
{: #ac-configure-rule-level-guarded-rollout}

To configure guarded rollout at the targeting rule level:

1. In the {{site.data.keyword.appconfig_short}} console, navigate to **Feature flags**.
2. Select the environment containing your feature flag.
3. Click the feature flag you want to configure.
4. In the **Targeting** section, select the rule you want to configure.
5. Ensure the rule has an overridden value attribute.
6. In the rule's **Rollout** section, select **Guarded** as the rollout type.
7. Follow steps 5–10 from the flag-level procedure above.

## Predefined rollout templates
{: #ac-guarded-rollout-templates}

{{site.data.keyword.appconfig_short}} provides predefined templates as starting points for common rollout durations. The default phase percentages for guarded rollout templates are set at or below 50%.

| Template | Total duration |
|----------|----------------|
| 1hr | 1 hour |
| 12hr | 12 hours |
| 24hr | 24 hours |
| 48hr | 48 hours |
{: caption="Predefined guarded rollout templates" caption-side="bottom"}

## Stopping a guarded rollout
{: #ac-stop-guarded-rollout}

You can stop a guarded rollout at any point. When stopped, {{site.data.keyword.appconfig_short}} removes the guarded rollout configuration, updates the rollout percentage to the percentage you specify at the time of stopping, and changes the rollout type to manual.

Use the appropriate API based on your rollout scope:

- **Stopping flag-level rollout**: Use the stop rollout API for feature flags.
- **Stopping rule-level rollout**: Use the stop rollout API for rules.

## Monitoring guarded rollouts
{: #ac-monitor-guarded-rollout}

You can monitor guarded rollout health from the feature flag details page in the {{site.data.keyword.appconfig_short}} console. Navigate to **Feature flags**, click the flag, and select the **Monitoring** tab.

The **Monitoring** tab is live while a guarded rollout is running and shows the following summary tiles:

- **Rollout type**: Displays **Guarded rollout** and the scope (feature flag or targeting rule).
- **State**: The current rollout state and active stage, for example Stage 1/2.
- **% Users served enabled value**: The percentage of users currently receiving the enabled variation.
- **Metric health**: A summary count of metrics in each health state — 🔴 Regression, ⚠️ Warning, ✅ Healthy.

The tab also displays a status banner when action is required:

| Banner | Meaning |
|--------|---------|
| **No events received** | No qualifying metric events have been received. Check that the event key in your metric matches the event key used in your application code, and that the flag is being evaluated by the client. |
| **Not enough data yet** | Events are being received but the sample size is not yet sufficient to evaluate the metric reliably. |
| **Regression detected** | A regression has been detected in one or more metrics. The rollout is paused at the current stage. Click **Continue with regression** to proceed to the next stage, or click **Rollback** to revert to 0%. |
{: caption="Monitoring status banners" caption-side="bottom"}

The **Metric charts** section displays a tab for each configured guardrail metric, showing the metric name, type, and direction. Each tab contains:

- **Summary panel**: Status, Absolute difference (New − Original), Certainty, and Metric events count.
- **Chart**: Absolute difference over time, with a 95% CI band, a zero baseline, and a new version estimate.
- **Results table**: Per-variation breakdown with Traffic, Metric events, Occurrence rate, CI Lower, and CI Upper columns.

### Historical rollout data
{: #ac-guarded-rollout-history}

After a guarded rollout ends, select the **Past Guarded Rollouts** tab to view historical snapshots including metric evaluation results, rollout configuration, relevant flag attributes, and rollback events.

### Notifications
{: #ac-guarded-rollout-notifications}

{{site.data.keyword.appconfig_short}} sends notifications through the {{site.data.keyword.en_short}} service integration when:

- A metric regression is detected and the rollout is paused (**Auto rollback** not enabled).
- An automatic rollback is triggered (**Auto rollback** enabled).
- Insufficient data is detected and the rollout rolls back to 0%.

To set up notification delivery channels such as email, SMS, or webhooks, see [Integrating with {{site.data.keyword.en_short}}](/docs/app-configuration?topic=app-configuration-ac-int-en).


You can also configure guarded rollout using the {{site.data.keyword.appconfig_short}} [API documentation](/apis/app-configuration).
