---

copyright:
  years: 2020, 2022
lastupdated: "2022-07-08"

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
{: codeblock}
