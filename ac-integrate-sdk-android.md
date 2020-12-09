---

copyright:
  years: 2020
lastupdated: "2020-12-09"

keywords: app-configuration, app configuration, integrate sdk, core sdk, android sdk, android, maven

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
{:curl: .ph data-hd-programlang='curl'}
{:node: .ph data-hd-programlang='node'}

# App Configuration service SDKs for Android
{: #ac-integrate-sdks-android}

{{site.data.keyword.appconfig_short}} service provides feature flags SDK, and crash insights SDK to integrate with your Android application. 
{:shortdesc}

## Integrating feature flag SDK
{: #ac-integrate-ff-sdk-android}

{{site.data.keyword.appconfig_short}} service provides feature flag SDK to integrate with your Android application. You can evaluate the values of your feature flag by integrating the feature flag SDK. 

<!-- placeholder for the steps -->
1. Install the sdks using 
1. In your Android application gradle file, include the sdk module with: 

### Examples
{: #ac-integrate-ff-example-android}

Refer to the below examples for using the feature related APIs.

#### Get all features
{: #ac-integrate-ff-get-all-features-android}

#### Get single feature
{: #ac-integrate-ff-get-single-feature-android}

#### Feature evaluation
{: #ac-integrate-ff-feature-evaluation-android}


#### Listen to the feature changes
{: #ac-integrate-ff-listen-feature-changes-android}

To listen to the data changes add the following code in your application

## Integrating Crash SDK
{: #ac-integrate-crash-sdk-android}

{{site.data.keyword.appconfig_short}} service provides crash insights SDK to integrate with your Android application. You can monitor and analyze the crashes and errors encountered in your application in the {{site.data.keyword.appconfig_short}} service dashboard by integrating the crash SDK.

### Reporting Android app crashes
{: #ac-integrate-crash-report-android-crashes}

#### Crash handling by using Android process events
{: #ac-integrate-crash-handling-android-process-events}

##### Unhandled errors
{: #ac-integrate-crash-unhandled-errors-android}

##### Unhandled promises
{: #ac-integrate-crash-unhandled-promises-android}


#### Android apps with Express framework
{: #ac-integrate-crash-android-apps-express-framework}


