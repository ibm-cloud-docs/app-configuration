---

copyright:
  years: 2025
lastupdated: "2025-07-18"

keywords: app-configuration, app configuration, experimentation, create an experiment

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Experimentation
{: #ac-experimentation}

As an app owner, experimentation functionality enables users to design and run experiments on their applications. It allows users to validate the impact of their feature flags. Users can create an experiment that lets you measure the effect of features on users by tracking various metrics that you set. 

By connecting these metrics to the feature flags in your environment, you can measure the changes in your customer’s behavior based on the different variations your application serves. 

The key features of experimentation include:

- Audience groups: Audience grouping for easy categorization is enabled, allowing users to easily categorize and identify target groups. 
- Advanced search and filtering: This enables users to quickly find relevant experiments and data, thereby improving efficiency in managing experiments. 
- Analytics and Visualization: Enhanced analytics and visualization enabling users to view how each variation is performing in accordance with each metric along with the probability that a variation performs better than the others.
- Enhanced Data Management: Organization and accessibility of experiments data is enhanced, allowing for better data handling and analysis.
- Integrations with existing entities: Experiments can be seamlessly integrated with {{site.data.keyword.appconfig_short}} entities such as environments, features, column, and segment. 

Experimentation functionality is available for users with Lite and Enterprise plans with limitations.
{: note}

## Steps to create an experiment
{: #ac-create-experiment}

The following steps indicate the process to create an experiment.

### Provide details for the experiment
{: #ac-details-experiments}
{: step}

1. From the left navigation pane, select **Experimentation**.

1. Under the **Design** tab, select **Create** in **Details**.

1. Provide a name and a hypothesis for your experiment. 

1. Select the environment and the Feature Flag for your experiment. To create a feature flag, see [Feature Flags](/docs/app-configuration?topic=app-configuration-ac-feature-flags#ac-create-feature-flag).

### Select audience for the experiment
{: #ac-audience-experiment}
{: step}

1. Select your audience.

There are 3 categories of audiences that you can select for your experiment:

- Everyone: The experiment is performed on all traffic that uses your application. 
- Targeted audience: You can select one of the targeted rules of the feature flag. Rules are the targeted segments of the feature flag. The experiment will only be performed on the traffic belonging to the selected segment. 
- Default flag audience: The experiment is performed on the traffic that does not belong to the targeted segments fall under the default audience.

The SDK integrated in your application runs an algorithm to determine the category to which an incoming user belongs, and based on this evaluation it serves the experimented variation or the default variation to the user.

1. Define your traffic distribution. 

Allocate the percentage of traffic for each variation. Variations are created in your feature flags, see [Creating a Variation](/docs/app-configuration?topic=app-configuration-ac-feature-flags#ac-create-variations-feature-flag). The audience of your experiment will be served the variation according to the percentage defined for each variant. For example, if you are performing an experiment on your e-commerce application, you can create variations to reflect the recommended products. If you set the traffic for product 1 as 30% and product 2 as 40%, then 30% of your audience will receive a recommendation for 1, and 40% will receive a recommendation for 2. The remaining 30%, who are not a part of the experimentation will receive a recommendation for any variant that you set. The traffic not a part of the experimentation will be classified into a control group.

You can choose to reassign the traffic in each iteration. This allows you to define whether the variation assigned to a user in the experiment iteration should remain the same or change in the next iteration. The variation assigned to a user in an iteration remains the same during an iteration.

### Set metrics for the experiment
{: #ac-experiment-metrics}
{: step}

Metrics measure the audience behavior affected by flags.You can create a metric from your experimentation dashboard or by selecting **Metrics** from the left navigation pane. 

1. Click **Create Metric**. 

1. Provide the name, description, event type, metric type, and event key. Currently {{site.data.keyword.appconfig_short}} only supports the custom event type and the conversion/binary metric type. 

The event key is used to define the metric you want to track. For example, if you are performing an experiment on your e-commerce application and you want to track whether a user clicks on a product, you define the event key as "user clicked". The event key can have a maximum of 100 characters.
{: note}

1. Once you have defined your metric click **Create**.

1. Navigate to your Experimentation dashboard, select the metric you want to track from the dropdown menu and click **Add+**. You can set only one metric as "Primary".

1. Once you have added all the metric you want to track, click **Start Experiment** to begin your experimentation.

#### Integrating Experimentation in your application SDK
{: #ac-integrating-experimentation-in-SDK}

To track your metrics, you need to integrate experimentation in your application SDK. You can integrate experimentation in the following SDKs :

1. Node.JS SDK: 

Record custom metrics for experiments by using the track function. Calling track queues the metric event, which will be sent in batches to the App Configuration servers.

```js
appConfigClient.track(eventKey, entityId)
```
Where

event key: The event key for the metric that is associated with the running experiment. The event key in your metric and the event key in your code must match exactly.

1. JS Client SDK:

Record custom metrics for experiments by using the track function. Calling track queues the metric event, which will be sent in batches to the App Configuration servers.

```js
appConfigClient.track(eventKey, entityId)
```

1. React SDK:

Record custom metrics by using the `useTrack` hook in experimentation.

```js
import { useTrack } from 'ibm-appconfiguration-react-client-sdk';

export default MyComponent = function () {
    const trackEvent = useTrack();
    return (
        <button onClick={() => trackEvent('clicked', 'user123')}>Buy</button>
    )
}
```

### Viewing results of the experiment
{: #ac-experiment-results}
{: step}

You can view the results of your experiment under the **Result** tab of your Experimentation dashboard. Once the audience of your experiment starts interacting with your application, you will be able to view the following:

- The experiment traffic for each variation that is the number of users encountering the variation. You can also download the data of the individual users. 
- The conversion rate of each variation according to a metric that is the number of users getting converted (doing the targeted action that is defined by the metric). For example selecting on product that is recommended as a part of your experiment.
- The probability to be best that is the likelihood that a particular variation outperforms all other variations for a specific metric. 

To view the results of previous iterations of your experiment, navigate to the **Iterations** tab of the Experimentation dashboard and select the iteration that you want to see the results of.


### Modifying {{site.data.keyword.appconfig_short}} entities while an experiment is running
{: #ac-entities-modification}

| Entity | Experiment running | Experiment stopped |
|--------|--------------------|--------------------|
| Experiment | **Update:** Blocked <br>**Delete:** Allowed | **Update:** Allowed <br>**Delete:** Allowed |
| Environment | **Update:** Allowed <br>**Delete:** Allowed | Update: Allowed <br>**Delete:** Allowed |
| Collection | **Update:** Allowed <br>**Delete:** Blocked | Update: Allowed <br>**Delete:** Allowed |
| Feature | **Update:** Allowed to name, description,tags,enabled values,disabled values, and rollout percentage. If `enabled` is set to false, it stops the experiment. Update to `collections` is blocked. Update to `segment rules` is allowed if type is `ALL` and if type is `RULE, update is blocked. <br>**Delete:** Allowed | **Update:** Allowed <br>**Delete:** Allowed |
| Segments | **Update:** Allowed to name, description, and tags. Update to `rules` is blocked.  <br>**Delete:** Blocked | **Update:** Allowed <br> **Delete:** Allowed |
| Variations | **Update:** Allowed to name and description. Update to `variation value` is blocked. <br>**Delete:** Blocked | **Update:** Allowed <br>**Delete:** Allowed |
| Metrics | **Update:** Allowed to name and description. Update to `event key` is blocked.  <br>**Delete:** Blocked | **Update:** Allowed <br>**Delete:** Allowed |
{: caption="Modifying entities" caption-side="bottom"}

