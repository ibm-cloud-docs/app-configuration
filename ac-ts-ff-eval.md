---

copyright:
  years: 2020, 2022
lastupdated: "2022-10-11"

keywords: app-configuration, app configuration, troubleshooting, faqs, Frequently Asked Questions, feature flag, evaluation

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

# The value returned for my targeted flag or property is not what I expected.
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
