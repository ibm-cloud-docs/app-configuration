---

copyright:
  years: 2022
lastupdated: "2022-06-14"

keywords: app-configuration, app configuration, about app configuration

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# How does {{site.data.keyword.appconfig_short}} work?
{: #ac-how-it-works}

Learn how {{site.data.keyword.appconfig_short}} works under normal operation or when something goes wrong.
{: shortdesc}

## Normal operation
{: #ac-normal-operation}

During normal operation, the {{site.data.keyword.appconfig_short}} SDK (#2 in Figure 1) handles the automatic delivery of the appropriate flag state or property value into your application from the {{site.data.keyword.appconfig_notm}} instance (#1 in Figure 1). During intialization, the SDK connects to the {{site.data.keyword.appconfig_short}} API and fetches the specified collections, segment rules, and targeting rules (#3 in Figure 1), and then evaluates the rules against attribute values programmed into your application to select the correct [segment](/docs/app-configuration?topic=app-configuration-ac-segments) and target values. Attributes upon which the rules operate are stored locally, and not in the {{site.data.keyword.appconfig_notm}} service on the cloud. Therefore, if you need to evalutate against attributes that are confidential, for example a social security number, the values never leave the local application environment.

After initialization, the application receives updated values in two ways depending on whether you are using server-side or client-side SDKs.  Server-side SDKs connect to the {{site.data.keyword.appconfig_short}} service through a web socket, and modified values are delivered your application in real time. Client-side SDKs pull values from the {{site.data.keyword.appconfig_short}} service upon a lifecycle change such being opened or brought to the foreground.

During normal operation, various metrics are sent back to the AC cloud service (#6 in Figure 1) so that the service can operate properly and so that you can monitor its operation.

![Overview](images/ac-how-it-works.png "How it works diagram"){: caption="Figure 1. How App Configuration works" caption-side="bottom"}

## Operation when something goes wrong 
{: #ac-something-goes-wrong}

As with any application or cloud service, sometimes things go wrong, but {{site.data.keyword.appconfig_notm}} continues to provide configurations even if the {{site.data.keyword.appconfig_notm}} service is unavailable to your app.

### Lost connection
{: #ac-lost-connection}

If the connection is lost between your application and the {{site.data.keyword.appconfig_notm}} service, the {{site.data.keyword.appconfig_notm}} SDK automatically falls back to a local cache file that contains the last known good configuration (#4 in Figure 1). In cache mode, changes to configurations that occur in the cloud do not reach the app, but the configuration that existed at the time of the lost connection continue to operate normally. 

As an extension of this case, assume that you need to operate your app an air-gapped environment. For that case, you can use a bootstrap config file (#5 in Figure 1). For more information on enabling offline mode, see [Enable offline mode](/docs/app-configuration?topic=app-configuration-ac-offline).

### Service down
{: #ac-service-down}

The likelihood of the {{site.data.keyword.appconfig_notm}} service going down is small. {{site.data.keyword.appconfig_short}} is deployed into multi-zone regions, meaning it runs across three geographically separate zones within a given region. If any zone goes down, the {{site.data.keyword.appconfig_notm}} service continues to operate normally. For more information on multi-zone regions, see [Region and data center locations for resource deployment](/docs/overview?topic=overview-locations).

In cases where you need extreme disaster recovery protection that spans regions, you can set up {{site.data.keyword.appconfig_notm}} instances in other regions and keep them in sync using the [{{site.data.keyword.appconfig_notm}} API](/apidocs/app-configuration).
