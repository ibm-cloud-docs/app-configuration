---

copyright:
  years: 2020, [{CURRENT_YEAR}]
lastupdated: "[{LAST_UPDATED_DATE}]"

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

Targeting assigns flag or property values to segments by evaluating rules.
{: tsCauses}

Targeting rules are executed in the order listed in the `Edit targeting` view. If a segment appears in more than one rule, only the value defined by the last rule is assigned.

Correct the order of evaluation by using the up- and down-arrows in the `Edit targeting` view, or remove the segment causing the unexpected outcome from rules.
{: tsResolve}
