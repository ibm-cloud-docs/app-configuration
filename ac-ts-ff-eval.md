---

copyright:
  years: 2020, 2026
lastupdated: "2026-05-18"

keywords: app-configuration, app configuration, troubleshooting, faqs, Frequently Asked Questions, feature flag, evaluation

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Why is the value returned for my targeted flag or property not what I expected?
{: #ac-troubleshooting-two}
{: troubleshoot}
{: support}

Feature flag is targeted with segment rules. Rule execution is not as expected.
{: tsSymptoms}

Targeting assigns flag or property values to segments by evaluating rules. Unexpected results can occur when segment logic, rule logic, or rollout behavior is misunderstood.
{: tsCauses}

To fix this issue, review how targeting is evaluated in the `Edit targeting` view, then update your segments or rules accordingly.
{: tsResolve}

- Within a segment, different attributes are evaluated with `AND`. For example, a segment with `environment is production` and `region is us-east` matches only when both conditions are true.
- Within a single segment attribute, multiple values are evaluated with `OR`. For example, `region is us-east, eu-de` matches if either value is true.
- Within a targeting rule, multiple segments are evaluated with `OR`. If any selected segment in that rule matches, the rule matches.
- Across targeting rules, the SDK evaluates rules by priority and applies the first matching rule.
- If no rule matches, a property returns its property value.
- If no rule matches for a feature flag, `enabled_value` is returned if the `entityId` falls into the `rollout_percentage`, and `disabled_value` is returned if the `entityId` does not fall into the `rollout_percentage`.

If the returned value is not what you expected, review the order of your rules and the segments included in each rule.

For example, if you want to enable a feature first for production users in `eu-de`, and later for production users in `us-east`, define each segment with all required attributes, such as:

- Segment 1: `environment is production` and `region is eu-de`
- Segment 2: `environment is production` and `region is us-east`

Then target those segments in separate rules and order the rules by priority in the `Edit targeting` view. This approach helps ensure that each rule matches only the intended audience.
