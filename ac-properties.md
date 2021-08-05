---

copyright:
  years: 2021
lastupdated: "2021-04-18"

keywords: app-configuration, app configuration, properties, property, create property

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

# Properties
{: #ac-properties}

You can create and manage properties, add them to collections and use them in your app by using SDKs. You can use them in your infrastructure by using Razee plugin or CLI. Using properties, you can manage the configuration properties of your infrastructure or applications centrally using {{site.data.keyword.appconfig_short}}.
{: shortdesc}

By default, the properties pane displays the list of properties in an environment that are created in the current {{site.data.keyword.appconfig_short}} service instance along with **Name**, **Value**, **Type** (boolean, numeric, string), date of creation, **Last evaluated**, **segments** that are targeted for the respective property.

An example usage of properties can be to decide the number of instances of your application in a specific region. To achieve this, create a property in {{site.data.keyword.appconfig_short}}, with type as numeric, and assign segments based on region value. 

![List of properties](images/ac-properties-default.png "List of properties"){: caption="Figure 17. List of properties" caption-side="bottom"}

## Create a property
{: #ac-create-properties}

To create a property, complete these steps:

1. In the {{site.data.keyword.appconfig_short}} console, click **Properties**. 
1. Select the **Current Environment**. This displays the list of properties in that environment.
1. Click **Create**. The side-panel opens with fields for creating a new property.

   ![Create property](images/ac-create-property.png "Creating property"){: caption="Figure 18. Creating a new property" caption-side="bottom"}

   ![Create peoperty with further details](images/ac-create-property1.png "Creating property further details"){: caption="Figure 19. Creating a property further details" caption-side="bottom"}

1. Provide the property details: 
   - **Name** - name of the property. 
   - **Property ID** - the property ID value is auto suggested based on the entered property name. You can modify the same, if needed. Use the **Property ID** value as the identifier in your SDK or API code.
   - **Property type** - specify the type of the property. Supported type includes: Boolean, String, and Numeric. For more information about property type and default values, refer [here](#selecting-properties-type).
   - **Default value** - specify the default value for the property type selected. For more information about property type and default values, refer [here](#selecting-properties-type).
   - Optionally, you can add the property to one or more collections by selecting in the **Add to collection** list.
   - **Description** - add a description of the property, which is optional.
   - Optionally, define **Tags** that are required to identify with the property.
1. Click **Create**.

## Selecting property type
{: #selecting-properties-type}

You can have one of the following property types that is associated to a property:
- Boolean
- String
- Numeric

Each of the **Property type** is having a default value. 
{: #property-type-default-value}

- The value for the **Property value** is required, which can be overridden while targeting to a segment.

### Boolean
{: #property-type-boolean}

When you select the **Property type** as *Boolean*, the **Default value** details are displayed:

![Property type - Boolean](images/ac-property-boolean.png "Selecting property type as boolean"){: caption="Figure 20. Property type - Boolean" caption-side="bottom"}

1. Select the **Property value** from the list. This is returned by default. This can be overridden while targeting to a segment.

### String
{: #property-type-string}

When you select the **Property type** as *String*, the **Default value** details are displayed:

![Property type - String](images/ac-property-string.png "Selecting property type as string"){: caption="Figure 21. Property type - String" caption-side="bottom"}

1. Specify the **Property value**. This is returned by default. This can be overridden while targeting to a segment.

### Numeric
{: #property-type-numeric}

When you select the **Property type** as *Numeric*, the **Default value** details are displayed:

![Property type - Numeric](images/ac-property-numeric.png "Selecting Property type as numeric"){: caption="Figure 22. Property type - Numeric" caption-side="bottom"}

1. Specify the **Property value**. This is returned by default. This can be overridden while targeting to a segment.

## Target collections to properties
{: #collection-target-properties}

You can add properties to one or more collections either during the creation of property or during editing a property details.

For adding collections to the properties, for the **Availability across collections** field, select the collection from the list.

If you try to target a property, that is not linked to a collection, a window is displayed to add a property to a collection.
{: note}

## Targeting a segment with properties
{: #targeting-segment-with-properties}

You can roll out property to one or more target segments. You can set different property values for different segments, if needed.

1. From the {{site.data.keyword.appconfig_short}} console, go to **Properties**. This displays the list of properties available in the current environment of the {{site.data.keyword.appconfig_short}} service instance.
1. Click **Add targeting** in the required property row. This displays **Target property to segments** side-panel.

   ![Target property to segments](images/ac-property-to-segments.png "Target property to segments"){: caption="Figure 23. Target property to segments" caption-side="bottom"}

1. Select **Segments** from the list. If there are no segments available to target, click **Create segment**. For more information about creating a segment, refer [here](/docs/app-configuration?topic=app-configuration-ac-segments#ac-create-segment).
1. Select the **Property value** (Inherit from property or Override).
1. Click **Save rule** to save the changes to the rules.
1. Click **Add targeting**.

If you try to target a property, that is not linked to a collection, a window is displayed to add a property to a collection.
{: note}

## Properties - overflow menu
{: #properties-overflow-menu}

The overflow menu for each of the property (three vertical dots) consists of **Edit**, **Copy**, and **Delete** operations and **Remove targeting** for already targeted property.

![Overflow menu for a property](images/ac-property-overflow-menu.png "Overflow menu for a property"){: caption="Figure 24. Overflow menu for a property" caption-side="bottom"}

* When **Edit** option is selected, you can make changes to the **Name**, **Description**, add or delete **Tags**, change the **Property type** and **Default value**, and add or remove collections for the **Availability across collections** field information.
* When **Copy** option is selected, the property information is copied and you need to modify the **Name** of the property. Optionally, modify the other details based on your need.
* When **Delete** option is selected, a confirmation window is displayed to seek confirmation to delete the selected property. Deleting option will permanently delete the property and the action cannot be undone.
* In the list of property, in a property, when **Copy to clipboard** icon is clicked, the property's **Property ID** value is copied to the clipboard.
* **Remove targeting** will remove the targeting of properties to a segment.
