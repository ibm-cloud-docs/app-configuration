---

copyright:
  years: 2020, 2025
lastupdated: "2025-02-07"

keywords: app-configuration, app configuration, troubleshooting, faqs, Frequently Asked Questions, question,

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# I used targeting to override flag and property values for a segment. Why are the default values still being applied?
{: #ac-troubleshooting-segment}
{: troubleshoot}
{: support}

Override values are not being assigned to segments.
{: tsSymptoms}

Attributes in your code may be missing or inconsistent with the attributes used in your segment rule.
{: tsCauses}

Segments are defined in the App Configuration service using attributes, and attributes are defined in your application code. If an attribute in a segment rule does not exist in your application, or has a value that is not part of the rule, then the app instance will not be recognized as part of a segment, and the default value will be assigned.

In your app code, include a JSON object that contains the various attribute values you want to use in your segment rules.
{: tsResolve}

Also, be sure the keys and values found in your app match the keys and values used in your App Configuration segment rule. See the following example.

```javascript
const entityId = "john_doe";
const entityAttributes = {
    'city': 'Bangalore',
    'country': 'India'
}
let feature = client.getFeature(<feature_id>);
let featureValue = feature.getCurrentValue(entityId, entityAttributes);
```
{: codeblock}

Entity attributes are used to evaluate if the entity is valid for the segment, and the corresponding value of the segment is returned for the feature flag.

The same fix is applicable for properties.
