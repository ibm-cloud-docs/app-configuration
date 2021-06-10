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

# Feature flag or property is evaluated with default values always and not according to segment rule definition?   
{: #ac-troubleshooting-segment}
{: troubleshoot}
{: support}
{:shortdesc}

{: tsSymptoms}
Feature flags are evaluated with default values and segments are not getting applied.  

{: tsCauses}
Segments are applied for the entity_attributes defined in the SDK. If entity_attributes are not defined, then default values are considered.

{: tsResolve}
Segments are defined with attribute names, values to consider and an operator.  
User can set a local JSON to be considered for evaluation:
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
