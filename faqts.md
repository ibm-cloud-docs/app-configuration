---

copyright:
  years: 2020, 2022
lastupdated: "2022-10-11"

keywords: app-configuration, app configuration, faqs, Frequently Asked Questions, question, billing, service

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Operations FAQs for {{site.data.keyword.appconfig_short}}
{: #ac-faqs-operations}

FAQs for {{site.data.keyword.appconfig_short}} provides answers to common operations issues for {{site.data.keyword.appconfig_short}}.
{: shortdesc}

## Can I get more evaluation behavior details with {{site.data.keyword.appconfig_short}} SDKs?
{: #faq-ac-eval}
{: faq}

Yes. Debugging can be enabled for {{site.data.keyword.appconfig_short}} SDK. As an example, use code `client.setDebug(true)`
to enable more traces for Node.js SDK. Refer to [SDK](/docs/app-configuration?topic=app-configuration-ac-sdks) documentation for specific SDKs.

## How can I get real-time updates of feature flag or properties in my application?
{: #faq-ac-updates}
{: faq}

Any update is pushed to the application in real time by the {{site.data.keyword.appconfig_short}} service. To listen to the changes, implement the following code in your Node.js application:

```javascript
client.emitter.on('configurationUpdate', () => {
   // add your code
   })
```

## What happens if resource collection is not enabled for the account as part of the Configuration aggregator and the user attempts to access configurations via the /configs query API?
{: #faq-ac-resource}
{: faq}

If resource collection is not enabled for the account and the user tries to access configurations using the /configs API, a 403 Forbidden error will be returned. The user needs to enable resource collection for the account to resolve this issue.

## How is the resource collection updated as part of the Configuration aggregator when new resources are added to or removed from IBM Cloud for onboard accounts?
{: #faq-ac-updated}
{: faq}

When new resources are added to or removed from IBM Cloud for onboarded accounts, the resource configuration will be updated automatically. If the changes are not updated within 24 hours, you can contact the IBM support.

## How can I troubleshoot client timeouts?
{: #faq-ac-troubleshoot}
{: faq}

- Check your internet connection: Ensure that your internet connection is stable and not experiencing  any disruptions.
- Verify server status: Confirm that App Configuration Service is available and no incidents have been reported.
- Adjust timeout settings: Some applications allow users to adjust timeout settings. If possible, consider extending the timeout duration to accommodate potential delays.
