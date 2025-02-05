---

copyright:
  years: 2023, 2025
lastupdated: "2025-01-31"

keywords: app-configuration, app configuration, context-based restrictions, access allowlist, network security

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Restricting access by network context
{: #ac-restrict-access-cbr}

[Context-based restrictions](/docs/account?topic=account-context-restrictions-whatis&interface=ui) provide a way for administrators to limit access to resources. What if certain data must be accessed from trusted networks only? A properly configured policy restricts all access to data unless the request originates from an approved [network zone](/docs/account?topic=account-context-restrictions-whatis&interface=ui#network-zones-whatis) and endpoint type (public, private, or direct).

To restrict access, you must be the account owner or have an access policy with the administrator role on all account management services.
{: note}

## Overview
{: #ac-cbr-overview}

To restrict access, you must create [zones](/docs/account?topic=account-context-restrictions-create&interface=ui#network-zones-create) and [rules](/docs/account?topic=account-context-restrictions-create&interface=ui#context-restrictions-create-rules).

First, create a zone with the appropriate details for network or resource definitions. Then, attach that zone to the specified resource to restrict access. You can create zones and rules by using a ReSTful [API](/apidocs/context-based-restrictions#introduction) or with [context-based restrictions](https://cloud.ibm.com/context-based-restrictions/overview){: external}. After you create or update a zone or a rule, it might take a few minutes for the change to take effect.

CBR rules do not apply to provisioning or deprovision processes.
{: note}

## Understanding network zones
{: #ac-cbr-network-zones}

By creating network zones, you can define an allowlist of network locations where access requests originate, to determine when a rule can be applied. The list of network locations can be specified by using IP addresses, such as individual addresses, ranges or subnets, and Virtual Private Cloud (VPC) IDs.

After you create a network zone, you can add it to a rule.

### Creating network zones by using the CBR API
{: #ac-cbr-create-zones-api}

The API supports defining [network zones](/apidocs/context-based-restrictions#introduction) by connecting to public (for example, cbr.cloud.ibm.com) and private endpoints (for example, private.cbr.cloud.ibm.com).

Use `GET /v1/zones` to list the zones. By using `POST /v1/zones`, you can create a new zone with the appropriate information. For more information, including a request body example, see [Creating network zones by using the API](/docs/account?topic=account-context-restrictions-create&interface=api#network-zones-create-api).

You can determine which services are available by checking for [reference targets](/apidocs/context-based-restrictions#list-available-serviceref-targets).
{: note}

After you create zones, you can [update](/apidocs/context-based-restrictions#replace-zone) or [remove](/docs/account?topic=account-context-restrictions-update&interface=api#network-zones-remove-api) them.

### Creating network zones by using the CBR UI
{: #ac-cbr-create-zone-ui}

After you set the prerequisites and requirements, you can create zones in the UI. For more information about the steps to follow, see [Creating context-based restrictions](/docs/account?topic=account-context-restrictions-create&interface=ui#network-zones-create).

Instead of creating a zone by using UI inputs, you can use the JSON code form to create a zone by clicking **Enter as JSON code**.
{: note}

After you create zones, you can [update](/apidocs/context-based-restrictions#replace-zone) or [remove](/docs/account?topic=account-context-restrictions-update&interface=ui#network-zones-remove) them.

## Understanding network rules
{: #ac-cbr-network-rules}

After you create your zones, you can attach the zones to your network resources by creating rules. When you add resources to a rule, you can choose from the available [types of endpoints](/docs/account?topic=account-context-restrictions-whatis#context-restrictions-endpint-type) that are specific to your network topology.

### Create network rules by using the CBR API
{: #ac-cbr-create-rules-api}

You can define network rules with the API by using the information that you collected from creating network zones.

By using `GET /v1/rules` with the endpoints that you chose, you can view a list of current rules. Use `POST /v1/rules` to create new rules. For more information, including a request body example, see [Creating rules by using the API](/docs/account?topic=account-context-restrictions-create&interface=api#context-restrictions-create-rules-api).

After you create rules, you can [update](/apidocs/context-based-restrictions#replace-rule) and [delete](/apidocs/context-based-restrictions#delete-rule) them.

### Creating network rules by using the CBR UI
{: #ac-cbr-create-rules-ui}

After you set the prerequisites and requirements, you can create zones in the UI. For more information about the steps to follow, see [Creating context-based restrictions](/docs/account?topic=account-context-restrictions-create&interface=ui#network-zones-create).

You can use the CBR UI to [add resources and contexts](/docs/account?topic=account-context-restrictions-create&interface=ui#context-restrictions-create-rules) to your network rules. Keep in mind the limitations.

Context-based restrictions check that an access request comes from an allowed context that you configure. Also, the rules might not take effect immediately due to synchronization and resource availability.
{: important}

After you create rules, you can [update](/apidocs/context-based-restrictions#replace-rule) and [delete](/apidocs/context-based-restrictions#delete-rule) them.

## Next steps
{: #ac-cbr-next-steps}

You must follow the creation or modification of zones or rules with adequate testing to ensure access and availability.

Users who attempt to access your resources outside of the defined zones receive `HTTP error 401` when the appropriate rules are not established.
{: note}
