---

copyright:
  years: 2020, 2025
lastupdated: "2025-07-18"

keywords: app-configuration, app configuration, create a feature flag, feature flags

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Targeting feature flags to segments
{: #ac-feature-flags}

As an app owner, create, and manage feature flags, add them to collections and use them in your app by using SDKs. You can also control the applicability of a feature by enabling or disabling it at run time.
{: shortdesc}

You can add an approval process flow for any configuration changes initiated through an {{site.data.keyword.appconfig_short}} environment by using the ServiceNow integration. The approval process flow is applicable to an {{site.data.keyword.appconfig_short}} environment like dev, stage, and production. For more information, see [Manage workflow](/docs/app-configuration?topic=app-configuration-ac-manage-workflow).

A feature can be enabled or disabled to all the collection users or to a specific set of users and devices or to a certain percentage of specific set of users and devices.

Feature roll outs can be coordinated by defining a start and end time and date. Also, choose a specific day on which a defined feature can be enabled or disabled.

By default, the **Feature flags** page displays the list of feature flags that are created in the current environment of the {{site.data.keyword.appconfig_short}} service instance along with details of the record like **Name**, **Type**, **Last Updated**, **Last Evaluated**, **Segments** that are targeted. Flag types are categorized as Boolean, Numeric, or String.

- A **Boolean** flag has two values and you can set the default value as 'true' or 'false'.
- A **String** type flag supports data in the form of text, and JSON or YAML files.
- A **Numeric** flag supports integers.

![List of feature flags](images/ac-list-feature-flag.png "List of feature flags"){: caption="List of feature flags" caption-side="bottom"}


## Watch and learn
{: #watch-and-learn-feature-flags}

![What are Feature Flags?](https://www.youtube.com/embed/AJa2B-twtG4){: video output="iframe" data-script="#feature-flags-concept-transcript" id="youtubeplayer" width="560" height="315" scrolling="no" allowfullscreen webkitallowfullscreen mozAllowFullScreen frameborder="0" style="border: 0 none transparent;"}

## Video transcript
{: #feature-flags-concept-transcript}
{: notoc}

What are Feature Flags?

Before you begin playing the video: In this video, the narrator draws representational images on the display board to explain the concept. [Draw] is used to represent when the narrator draws the representational image. [Writing] is used to represent when the narrator writes some text.

What if you could release a feature to different groups of users without deployment?
Is there a way to effectively test features in production, and immediately roll them back if needed?

I'll be answering those questions by discussing feature flags, or sometimes referred to as feature toggle, or switches.

Feature flags are conditions that encompass feature code that allow you to flip them on and off at will.
Okay, let's use an example.
[Draw] Let's say we've got an ice cream shop franchise that's looking to expand to a new city and we've got a
[Draw] banner that we want to display on our website. We'll call this open banner.
We only want to display this banner to users that are [Draw] nearby our new ice cream shop we can do this by using feature flags.

There's a couple benefits to using feature flags.
[Writing] Number one is we can actually turn these on or off without deployment.
[Writing] Number two is we can actually test directly in production.
[Writing] And number three we can segment our users based on different attributes.

Okay, there's a couple ways you can do this one way is by using properties in JSON files or config maps. There's a better way however by using a feature flag service.

[Writing] There's a couple benefits to using a feature flag service. Number one is you can have essentially managed place for your features, or excuse me your feature flags.
[Writing] Number two is you can turn these on and off  without modifying your properties in your future, in your apps or web pages.
[Writing] And number three is you get audit and usage data. It's harder to get the audit and usage data by using JSON files.

Okay, so now let's go back to our example we've got our open banner feature and now let's wrap it with some feature flag code.

And so here's an example, kind of pseudo code, that you can use if store open is enabled.

[Writing] if (storeopen is Enabled()){
Then we're going to show open banner
[Writing] show Open Banner();}

so this pseudocode represents our feature code and the flag that potentially could encompass it.

Now let's actually put this in production and [Draw] make it show showcase to some users.

So now that we've got our feature in production it's not usable to any users right now this is an idea typically displayed with feature flags called dark launch. Dark launch is when a feature is in production but not visible to any or all users or any or some users, excuse me.

Now we want to introduce the idea of [Writing] segments.

So we've already said that we only want a certain number of people to view this, people who are nearby our new shop. This will be our segment A, and a segment is simply users or groups of users that have attributes tied to them.

So this first one might have [Writing] current location, and [Writing] zip code.

Attributes, this allows users who are either currently in the location or have already stipulated that they live nearby to view this feature, but before we do that we want to test the feature out on our own employees. [Writing] So we would have segment Bof our testers because we want them to be our employees the attribute might be [Writing] email ID.

Now we can effectively test our feature in production by {Draw] flipping this toggle on. So now this feature is on for our testers, and say maybe something went wrong so we're actually going to flip it off fix it, and then we'll turn it back on for segment B.

Once we're satisfied that everything is working well. Then we can flip this on for our [Draw] segment A.

Now all this is done without a deployment because our feature is already in production. All we're doing is making it visible or not visible to certain users.

Once it is in production. [Draw] We can actually add a little bit of automation to this

with our testers, we did it manually, we flipped it on and off manually, but with feature flags we can actually add a time element. So let's say we only want this to be viewable for [Writing] three weeks,

two weeks before grand opening, one week after grand opening of our new shop. This will be flipped on and then automatically turned off or not visible for this segment of users after three weeks.

Okay, so now we're getting really good at using feature flags so our [Draw] feature flags are potentially starting to stack up we might have a couple apps and a couple websites with a couple different types of features that are flagged.

So we've got maybe [Writing] app one here, [Writing] app two, and say a [Writing] web page.

With a feature flagging service we can actually group these in collections so that we're a little bit more organized with which feature flags are tied to, which apps are web pages.

So now today we've learned about returning feature flags on and off without deployment testing directly in production, and then segmenting those features based on the user attributes.

Thank you for watching. If you have questions, please drop us a line below. If you want to see more videos like this in the future, please like and subscribe. And don't forget, you can grow your skills and earn badges with IBM CloudLabs, which are free browser-based interactive kubernetes labs.

## Create a feature flag
{: #ac-create-feature-flag}

To create a feature flag, complete these steps:

1. In the {{site.data.keyword.appconfig_short}} console, click **Features flags**.

1. Select the **Current Environment** to display the list of feature flags in that environment.

1. Click **Create**. The side panel opens with fields for creating a new feature flag.

   ![Create feature flag](images/ac-create-feature-flag.png "Creating feature flag"){: caption="Creating a new feature flag" caption-side="bottom"}

1. Provide the feature flag details:
   - **Name** - name of the feature flag.
   - **Feature flag ID** - the feature flag ID value is auto suggested based on the entered feature name. You can modify the same, if needed. Use the **Feature flag ID** value as the identifier in your SDK or API code.
   - **Flag type** - specify the type of the feature flag. Supported type includes: Boolean, String, and Numeric. For more information about flag type and default values, see [Selecting feature flag type](#selecting-feature-flag-type).
   - **Default value** - specify the default value for the feature flag type selected. For more information about flag type and default values, see [Selecting feature flag type](#selecting-feature-flag-type).
   - Optionally, select a collection for applying a feature flag now. Otherwise, you need to add a collection before you toggle a feature flag. You can add the feature flag to one or more collections by selecting in the **Flag availability across collections** list.
   - **Feature rollout** - specify the `Rollout percentage` by using the slider. For more information about percentage rollout, see [Configure feature rollout percentage](#configure-rollout-percentage).
   - **Description** - add a description of the feature flag, which is optional.
   - Optionally, define **Tags** that help you to identify the feature flag.

1. Click **Create**.

By default, when you create a new feature flag, the **Enabled** toggle switch is set to `OFF`.
{: note}

## Selecting feature flag type
{: #selecting-feature-flag-type}

You can have one of the following flag types that is associated to a feature flag:
- Boolean
- String
- Numeric

Each of the Flag type is having a default value.
{: #flag-type-default-value}

- When you set the toggle switch to *ON*, the value for the **Enabled value** is required, which can be overridden when targeting to a segment.
- When you set the toggle switch to *OFF*, the value for the **Disabled value** is required, which can be overridden when targeting to a segment.

### Boolean
{: #feature-flag-type-boolean}

When you select the **Flag type** as *Boolean*, the **Default value** details are displayed:

![Feature flag type - Boolean](images/ac-feature-flag-boolean.png "Selecting feature flag type as Boolean"){: caption="Feature flag type - Boolean" caption-side="bottom"}

1. Select the **Enabled value** from the list. This value is returned by default when the toggle switch is set to *ON* for the feature flag. This value can be overridden when targeting to a segment.

1. Select the **Disabled value** from the list. This value is returned by default when toggle switch is set to *OFF* for the feature flag.

### String
{: #feature-flag-type-string}

When you select the **Flag type** as *String*, the **Default value** details are displayed:

![Feature flag type - String](images/ac-feature-flag-string.png "Selecting feature flag type as string"){: caption="Feature flag type - String" caption-side="bottom"}

1. Select the **Format** of the string flag type from the list. Supported format is Text, JSON, and YAML. When JSON or YAML format is selected, provide the **Enabled value** and **Disabled value** in the selected format.

1. Specify the **Enabled value**. This value is returned by default when toggle switch is set to *ON* for the feature flag. This value can be overridden when targeting to a segment.

1. Specify the **Disabled value**. This value is returned by default when toggle switch is set to *OFF* for the feature flag.

### Numeric
{: #feature-flag-type-numeric}

When you select the **Flag type** as *Numeric*, the **Default value** details are displayed:

![Feature flag type - Numeric](images/ac-feature-flag-numeric.png "Selecting feature flag type as numeric"){: caption="Feature flag type - Numeric" caption-side="bottom"}

1. Select the **Enabled value** from the list. Only integer values are supported. This value is returned by default when toggle switch is set to *ON* for the feature flag. This value can be overridden when targeting to a segment.

1. Select the **Disabled value** from the list. Only integer values are supported. This value is returned by default when toggle switch is set to *OFF* for the feature flag.

## Target collections to feature flags
{: #collection-target-feature-flags}

Optionally, select a collection for applying a feature flag now. Otherwise, you need to add a collection before you toggle a feature flag.
You can add feature flags to one or more collections either during creation of feature flag or during editing feature flag details.

For adding collections to the feature flag, for the **Flag availability across collections** field, select the collection from the list.

If you try to target a feature flag that is not linked to a collection, a window is displayed to add a feature flag to a collection.
{: note}

## Configure feature rollout percentage
{: #configure-rollout-percentage}

You can configure the feature flag with a rollout percentage in the range of 0 to 100, denoting the applicability of the feature to a partial set of users or devices.

Percentage rollout helps to enable a feature to a small percentage of random users or subset of entities, providing more control on the release cycle and achieve progressive delivery. When you are confident on the feature that you want to roll out is working as intended, increase the percentage over time.

Percentage rollout uses a hashing algorithm that generates a hash based on the rule set. This hash is used by the SDK to generate a percentage value for that user. The percentage value generated for that user is compared to the value set for the percentage rollout value, determines whether the user is eligible to receive that feature or not.

For example, the hash has partitions from 1 to 100,000. When you assign a feature flag, the hash assigns values from 1 to 100,000 to users in each partition. For example, when you assign 25% to a feature flag, {{site.data.keyword.appconfig_short}} SDK delivers that feature to hash partitions from 1 to 25,000. If you change the percentage of users receiving that feature from 25% to 50%, partitions 25,001 to 50,000 would be added to the set of partitions already receiving that feature.

Percentage rollout capability is available for Lite and Enterprise plans.
{: note}

Following are some of the percentage rollout scenarios:

- If the feature flag is disabled, then SDK returns the default **Disabled value**.
- If the feature flag is enabled without any segment rules and no percentage rollout is set, then the SDK returns default **Enabled value**.
- If the feature flag is enabled without any segment rule and percentage rollout is set to 0%, then the SDK returns **Disabled value** for all users.
- If the feature flag is enabled without any segment rule and percentage rollout is set to a percent, say 50%, then the SDK checks if the user belongs to the configured percentage rollout size, if the user belongs to the rollout criteria, then the SDK returns the **Enabled value**. If the user doesn't belong to the rollout criteria, then the SDK returns the **Disabled value**.
- If the feature flag is enabled with segment rules, then SDK first evaluates the user against the configured rules. If user is part of the configured rule, then the SDK evaluates if the user is eligible for percentage rollout.
   - If multiple rules are configured and the user is checked for rule match until the first match. If no match found, then the SDK evaluates against the default rollout.
   - If the user is evaluated to be part of the segment and the segment percentage rollout is 0%, then even if the user is part of the segment, user will not receive the segment value. The SDK returns the default **Disabled value**.
   - If the user is evaluated to be part of the segment and the segment percentage rollout is set to a percentage, say 50%, then the SDK checks if the user belongs to configured rollout size, if the user belongs to the rollout criteria, then the SDK returns the segment overriding value. If the user doesn't belongs to the rollout criteria, then the SDK returns **Disabled value**.

### View as table
{: #feature-flags-percentage-rollout-scenarios}
{: notoc}

| Feature Flag | Is targeting configured? | Percentage  \n rollout | Is user  \n part of  \n configured segment | Is user  \n part of  \n percentage rollout \n criteria | Value  \n returned  \n by SDK |
| :---------- | :---------- | :---------- | :---------- | :---------- | :---------- |
| Disabled | NA | Any % rollout set | NA | NA | Disabled value |
| Enabled  | No | 0% | NA | No | Disabled value |
| Enabled  | Yes | 0% | Yes | No | Disabled value |
| Enabled  | Yes | 0% | No | No | Disabled value |
| Enabled  | No | Between 0% to 100% | NA | Yes | Enabled value |
| Enabled  | No | Between 0% to 100% | NA | No | Disabled value |
| Enabled  | Yes | Betweeen 0% to 100% | Yes | Yes | Overriden value |
| Enabled  | Yes | Betweeen 0% to 100% | Yes | No | Disabled value |
| Enabled  | Yes | Between 0% to 100% | No | Yes | Enabled value |
| Enabled  | Yes | Between 0% to 100% | No | No | Disabled value |
| Enabled  | No | 100% | NA | Yes | Enabled value |
| Enabled  | Yes | 100% | Yes | Yes | Overriden value |
| Enabled  | Yes | 100% | No | Yes | Enabled value |
{: caption="Percentage rollout scenarios" caption-side="bottom"}

## Targeting a segment with a feature flag
{: #targeting-segment-with-feature-flag}

You can roll out feature flags to one or more target segments. You can set different flag values for different segments, if needed.

1. From the {{site.data.keyword.appconfig_short}} console, go to **Feature flags**. This pane displays the list of feature flags available in the current environment of the {{site.data.keyword.appconfig_short}} service instance.

1. Click **Add targeting** in the required feature flag row to display the **Target flag to segments** side-panel.

   ![Target flag to segments](images/ac-feature-flag-to-segments.png "Target flag to segments"){: caption="Target feature flag to segments" caption-side="bottom"}

1. The **Feature rollout** displays the default **Rollout percentage** slider define when creating the feature flag. Modify the rollout percentage value, if required.

1. In the **Rules** section, define the rule by specifying the following:

   - In the **Rollout percentage**, you can define the value as an **Override** or **Inherit from default**. If the **Override** option is selected, then specify the **Rollout percentage** override value by using the slider.
   - Select **Segments** from the list. If no segments are available to target, click **Create segment**. For more information about creating a segment, see [Create a segment](/docs/app-configuration?topic=app-configuration-ac-segments#ac-create-segment).
   - For the **Enabled value**, you can select **Override** and modify the value or select **Inherit from flag**.
   - Click to **Save rule**

   You can define more rules by clicking **Add rule**.

1. Click **Add targeting**.

If you try to target a feature flag that is not linked to a collection, a window is displayed to add a feature flag to a collection.
{: note}

## Creating Variations for Experimentation
{: #ac-create-variations-feature-flag}

Add variations to your feature flag to support experimentation. The variants added to a feature flag help you track how different variations of your application are performing when an experiment is conducted using the feature flag. This helps you identify which variation performs the best.

To create a variation:

1. Navigate to your {{site.data.keyword.appconfig_short}} instance. To learn the process to create an {{site.data.keyword.appconfig_short}} instance, see [Creating an App Configuration service instance](/docs/app-configuration?topic=app-configuration-ac-create-an-instance).

1. In the {{site.data.keyword.appconfig_short}} console, click **Features flags**.

1. Select the **Current Environment** to display the list of feature flags in that environment.

1. Click **View Variations** on the feature you intend to use for experimentation.

1. Click **Create**.

1. Provide the name,value and description for your variation.

1. Click **Create**.

## Enabling a feature flag
{: #enabling-feature-flag}

After you target a feature flag to a segment, click the toggle (ON/OFF) to enable or disable a feature flag.



## Feature flags - overflow menu
{: #feature-flags-overflow-menu}

The overflow menu for each of the feature flag (three vertical dots) consists of **Edit**, **Copy**, and **Delete** operations and **Remove targeting** for those feature flags that are already targeted.

![Overflow menu for a feature flag](images/ac-feature-flag-overflow-menu.png "Overflow menu for a feature flag"){: caption="Overflow menu for a feature flag" caption-side="bottom"}

- When **Edit** option is selected, you can change the **Name**, **Description**, add or delete **Tags**, change the **Flag type** and **Default value**, and add or remove collections for the **Flag availability across collections** field information.
- When **Copy** option is selected, the feature flag information is copied, and you need to modify the **Name** of the feature flag. Optionally, modify the other details based on your need.
- When **Delete** option is selected, a confirmation window is displayed to seek confirmation to delete the selected feature flag. Deleting option permanently deletes the feature flag and the action cannot be undone.
- In the list of feature flags, in a feature flag, when **Copy to clipboard** icon is clicked, the feature flag's **Feature flag ID** value is copied to the clipboard.
- **Remove targeting** removes the targeting of feature flags to a segment.
