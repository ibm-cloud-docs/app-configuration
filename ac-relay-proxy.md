---

copyright:
  years: 2026
lastupdated: "2026-07-31"

keywords: app-configuration, app configuration, relay proxy, proxy, air-gap, sdk, websocket, sse, failover, seed file

subcollection: app-configuration


---

{{site.data.keyword.attribute-definition-list}}

# Relay Proxy
{: #ac-relay-proxy}

The {{site.data.keyword.appconfig_short}} Relay Proxy sits between your SDK clients and the {{site.data.keyword.appconfig_notm}} service. Instead of every SDK connecting directly to {{site.data.keyword.cloud_notm}}, SDK clients connect to the proxy within your own network. The proxy fetches and caches configuration from {{site.data.keyword.appconfig_notm}}, then delivers it to all connected clients.
{: shortdesc}

## Why use the Relay Proxy?
{: #ac-relay-proxy-why}

Consider using the Relay Proxy in the following scenarios:

- **Reduce outbound calls to {{site.data.keyword.cloud_notm}}** — The proxy opens one upstream connection per configured collection and environment combination regardless of how many SDK instances are deployed in your fleet.
- **Air-gap or private-network deployments** — SDK clients communicate only with the proxy inside your network. The proxy handles all connectivity to {{site.data.keyword.cloud_notm}}.
- **Single point of authentication** — One IBM Cloud IAM API key is required on the proxy. SDK clients authenticate to the proxy using a key that you define.
- **Primary and backup instance failover** — The proxy automatically switches to a backup {{site.data.keyword.appconfig_notm}} instance when the primary is unavailable, and recovers automatically.
- **Graceful start from a local seed file** — In fast-start mode, the proxy serves configuration immediately from a local seed file while fetching fresh data from {{site.data.keyword.cloud_notm}} in the background.

## How SDK clients connect to the Relay Proxy
{: #ac-relay-proxy-sdk-connections}

SDK clients use the same connection types they use to connect directly to {{site.data.keyword.appconfig_notm}}, but they target the proxy host and port instead:

| SDK type | Connection type | Purpose |
|---|---|---|
| Server SDKs | WebSocket | Receive real-time configuration change events |
| Client SDKs | Server-Sent Events (SSE) | Receive configuration snapshots and updates |
| All SDKs | REST | Fetch initial configuration |
{: caption="SDK connection types to the Relay Proxy" caption-side="bottom"}

## Connection multiplexing
{: #ac-relay-proxy-multiplexing}

One of the primary benefits of the Relay Proxy is connection multiplexing. Hundreds or thousands of SDK instances can connect to the proxy, but the proxy opens only one upstream WebSocket connection per `collection × environment` combination to {{site.data.keyword.appconfig_notm}}. That upstream connection count is fixed by your configuration and never grows with your fleet size.

For example, if you configure two collections (`inventory` and `payments`) each used in two environments (`dev` and `prod`), the proxy maintains exactly four upstream WebSocket sessions regardless of how many SDK instances connect to it:

| Upstream WebSocket session | Collection | Environment |
|---|---|---|
| Session 1 | inventory | dev |
| Session 2 | inventory | prod |
| Session 3 | payments | dev |
| Session 4 | payments | prod |
{: caption="Example upstream WebSocket sessions for two collections and two environments" caption-side="bottom"}

When {{site.data.keyword.appconfig_notm}} sends a change event on an upstream connection, the proxy fans it out instantly to all SDK clients subscribed to that combination.

Each `collection × environment` combination has its own isolated cache slot and upstream WebSocket session inside the proxy.
{: note}

## Startup modes
{: #ac-relay-proxy-startup-modes}

The Relay Proxy supports two startup modes depending on whether a seed file is configured.

### Normal start
{: #ac-relay-proxy-normal-start}

In normal start mode, the proxy must successfully contact {{site.data.keyword.appconfig_notm}} before it serves any request. If any configuration fetch fails, startup aborts. This mode guarantees that clients always receive authoritative data from their first request.

The startup sequence is as follows:

1. Fetch configuration from {{site.data.keyword.appconfig_notm}} — all configured combinations are fetched synchronously.
1. Cache all configurations in memory.
1. Start the HTTP server and accept client requests.
1. Open upstream WebSocket sessions for live change notifications, one per combination.

### Fast start
{: #ac-relay-proxy-fast-start}

In fast-start mode, a seed file pre-warms the cache so the proxy can start serving requests immediately, without waiting for {{site.data.keyword.cloud_notm}}. Fresh configuration is fetched in the background and pushed to all already-connected clients when available. This mode is suited to air-gap environments and resilient deployments.

The startup sequence is as follows:

1. Load the seed file from disk — the cache is pre-warmed instantly, no network call required.
1. Start the HTTP server immediately.
1. Fetch fresh configuration from {{site.data.keyword.appconfig_notm}} in the background — overwrites seed data and notifies all connected clients.
1. Open upstream WebSocket sessions for live change notifications, one per combination.

For the seed file format and configuration options, see the [App Configuration API reference](https://{DomainName}/apidocs/app-configuration){: external}.

## How a configuration change reaches your SDKs
{: #ac-relay-proxy-change-propagation}

When a configuration change is published in the {{site.data.keyword.appconfig_short}} console, the change reaches your SDK clients through the following sequence:

1. {{site.data.keyword.appconfig_notm}} sends a WebSocket message to the proxy on the relevant upstream session.
1. The proxy re-fetches the updated configuration for that combination and stores it in the cache.
1. The proxy broadcasts the updated configuration to all connected clients:
   - Server SDKs receive a WebSocket event.
   - Client SDKs receive an SSE event with the updated configuration payload.

## Primary and backup failover
{: #ac-relay-proxy-failover}

When a backup instance is configured, the proxy provides automatic failover for WebSocket sessions and configuration fetches.

- **WebSocket sessions** — Each combination maintains its own upstream WebSocket. When the primary instance becomes unavailable, the proxy immediately connects to the backup. The proxy retries the primary instance every 15 seconds and closes the backup connection as soon as the primary recovers.
- **Configuration fetches** — HTTP configuration fetches follow a primary-then-backup order.

## Pointing your SDKs at the Relay Proxy
{: #ac-relay-proxy-sdk-setup}

To connect your SDK clients to the Relay Proxy instead of directly to {{site.data.keyword.cloud_notm}}:

1. Replace the {{site.data.keyword.cloud_notm}} hostname in your SDK initialization with the proxy's host and port.
1. Region, guid, API key, collection_id and environment_id should be same as what passed in the relay proxy configuration.

No other SDK code changes are required.

To get started with the Relay Proxy, reach out to {{site.data.keyword.appconfig_short}} support.
{: note}
