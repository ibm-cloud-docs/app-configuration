---

copyright:
  years: 2020
lastupdated: "2020-11-11"

keywords: app-configuration, app configuration, troubleshooting, faqs, Frequently Asked Questions, question,

subcollection: app-configuration

---

{:codeblock: .codeblock}
{:external: target="_blank" .external}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:tip: .tip}
{:java: .ph data-hd-programlang='java'}
{:ruby: .ph data-hd-programlang='ruby'}
{:c#: .ph data-hd-programlang='c#'}
{:objectc: .ph data-hd-programlang='Objective C'}
{:python: .ph data-hd-programlang='python'}
{:javascript: .ph data-hd-programlang='javascript'}
{:php: .ph data-hd-programlang='PHP'}
{:swift: .ph data-hd-programlang='swift'}
{:reactnative: .ph data-hd-programlang='React Native'}
{:csharp: .ph data-hd-programlang='csharp'}
{:ios: .ph data-hd-programlang='iOS'}
{:android: .ph data-hd-programlang='Android'}
{:cordova: .ph data-hd-programlang='Cordova'}
{:xml: .ph data-hd-programlang='xml'}
{:new_window: target="_blank"}
{:table: .aria-labeledby="caption"}
{:deprecated: .deprecated}
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:term: .term}
{:troubleshoot: data-hd-content-type='troubleshoot'}

#  I have used targeting to override flag and property values for a segment, but the default values are still being applied.  
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

Also, be sure the keys and values found in your app match the keys and values used in your App Configuration segment rule. See example below.
```javascript
const entityId = "john_doe";
const entityAttributes = {
    'city': 'Bangalore',
    'country': 'India'
}
let feature = client.getFeature(<feature_id>);
let featureValue = feature.getCurrentValue(entityId, entityAttributes);
```
{:codeblock: .codeblock}
Entity attributes are used to evaluate if the entity is valid for the segment, and the corresponding value of the segment is returned for the feature flag.

The same fix is applicable for properties.
