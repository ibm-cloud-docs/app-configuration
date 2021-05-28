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

# Does deleting a feature flag or property in an environment delete it across all environments?
{: #ac-troubleshooting-del}
{: troubleshoot}
{: support}
{:shortdesc}

{: tsSymptoms}
Deleting a feature flag or property in an environment deletes it for all environments.

{: tsCauses}
Feature flag or property is available to all environments. Updates to values are per environment. Create and delete action executes across all environments.

{: tsResolve}
Deletion of feature flag or property is across all environments. If a flag is not required in a particular environment, disable the flag or set the values default. If a flag is not required in any environment, it can be deleted.

