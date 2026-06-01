---

copyright:
  years: 2026
lastupdated: "2026-06-01"

keywords: app-configuration, app configuration, askai, cloud assistant, query resources, configuration aggregator

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# AskAI: Cloud resource query assistant
{: #ac-askai}

AskAI is an intelligent cloud assistant that helps you query aggregated cloud resource configurations.
{: shortdesc}

AskAI is currently in beta.
{: note}


## Accessing AskAI
{: #ac-askai-access}

Access the AskAI interface through the Configuration aggregator page in your App Configuration instance.

To access your AskAI assistant:

1. In the IBM Cloud console, click **Menu** ![Menu](images/icon_hamburger.svg) > **Resource List** > **Developer Tools** > your App Configuration instance.
2. Click **Configuration aggregator** in the navigation pane.
3. Click **AskAI** to open the AskAI interface.

## AskAI Capabilities
{: #ac-askai-capabilities}

AskAI provides powerful features for querying, managing, and exporting your cloud resource configuration data.

AskAI supports the following capabilities:

### Creating and managing chats
{: #ac-askai-create-chats}

Organize your queries by creating and managing multiple chat sessions.

Create chats to ask questions about your aggregated resource configurations. Answers are displayed in a tabular format, making results easier to view and analyze.

- **New chat**: Click **+** to create a new chat. Chats are automatically named sequentially, such as Chat 1 and Chat 2.
- **Chat history**: View your previous chats in the left pane under **Chat history**.
- **Search chats**: Use the search bar to find specific chats by name or query.
- **Rename chat**: Select a chat from the history and rename it for better organization.
- **Delete chat**: Remove chats that you no longer need from the menu options.
- **Run again**: Each chat displays your most recent query with a retry option so that you can quickly rerun it.


Chat history preserves only the last query for each chat. Full conversation history isn't maintained. When you refresh the page or return to a chat, only the most recent question is available.
{: important}

### Querying and viewing results
{: #ac-askai-querying-viewing-results}

Ask natural language questions and view results in an organized table format.

- **Natural language queries**: Ask questions about your cloud resources in natural language.
- **Tabular results**: Answers are displayed in an easy-to-read table with 10 records per page.
- **Response summary**: View AI-generated summaries alongside the table data.
- **Long query notification**: For queries that take longer than 20 seconds, a loading message indicates that processing is in progress.
- **Latest results only**: Only the most recent query result in a chat supports interactive features, such as pagination and downloads. Older results in chat history are view-only.

### Pagination
{: #ac-askai-pagination}

Browse through large result sets using pagination controls.

Navigate to different pages in the table when more records are available. Use the pagination controls to browse large result sets efficiently.

- **Navigate pages**: Use the pagination controls at the bottom of the table to browse results.
- **Page size**: Results display 10 records per page.
- **Page indicators**: View the current page number and total record count.
- **Restriction**: Only the latest query result supports pagination. Older results in chat history can't be paginated.


### Downloading results
{: #ac-askai-download}

Export query results in JSON or CSV format for offline analysis.

Download results when you need to export large datasets for further analysis or reporting.

- **Download all**: Click the **Download All** menu in the table header.
- **File formats**: Choose JSON or CSV format.
- **Job submission**: Downloads are processed as background jobs that you can track in the **Jobs** section.
- **Restriction**: Only the latest query result in a chat supports downloads.

### Job management
{: #ac-askai-job-management}

Track and manage your download jobs with automatic status updates.

View and manage your download jobs from the **Jobs** section in the left pane. The interface displays up to 10 recent jobs.

#### Job status indicators
{: #ac-askai-job-status}

Monitor the progress of your download jobs through various status states.

- **Pending**: The job is queued for processing.
- **In progress**: The job is currently being processed. Status refreshes automatically every 60 seconds.
- **Completed**: The job is ready for download. Click the download icon to retrieve your file.
- **Downloaded**: The job has been downloaded successfully to your device.
- **Failed**: Job processing failed. You might need to rerun the query.
- **Unavailable**: Job results are no longer available because they expired after 12 hours.

#### Job features
{: #ac-askai-job-features}

Manage download jobs with automatic polling and time-limited result availability.

- **Auto-polling**: Active jobs, such as Pending and In progress, automatically check for status updates every 60 seconds.
- **Download results**: Click the download icon ![Download](images/download.svg) when the status is **Completed**.
- **Job history**: View up to 10 recent jobs.
- **Result expiration**: Results are available for **12 hours** after completion. After that period, they are deleted automatically and you must rerun the query.


### Accessing documentation
{: #ac-askai-documentation-access}

Access help resources and FAQs directly from the chat interface.

Click the menu icon in the chat header and select **Documentation** to access help resources and FAQs.


### List of supported resources
{: #ac-askai-supported-resources}

Query configurations across a wide range of IBM Cloud services and resources.

AskAI supports queries for the following IBM Cloud services and configuration types:

- **Virtual Server Instance (VSI)** - Virtual machines
- **Code Engine** - Serverless container platform instances
- **Image** - Operating system images
- **VPC (Virtual Private Cloud)** - Virtual network instances
- **Subnet** - Network subnets
- **Load Balancer** - Load balancing configurations
- **VPN (Virtual Private Network)** - VPN gateways
- **Public Gateway** - Public gateway configurations
- **Security Group** - Security group rules
- **Flow Log Collector** - Network flow logs
- **Direct Link** - Private cloud connectivity
- **Block Storage** - Block storage volumes
- **File Storage** - File storage shares
- **Snapshot** - Storage snapshots
- **Databases for Elasticsearch** - Elasticsearch instances and tasks
- **Databases for MongoDB** - MongoDB instances and tasks
- **Databases for MySQL** - MySQL instances and tasks
- **Databases for PostgreSQL** - PostgreSQL instances and tasks
- **Databases for Redis** - Redis instances and tasks
- **IAM Access Groups** - Access group configurations
- **IAM Identity** - Profiles, API keys, service IDs, CBR resources, global catalog resources
- **App ID** - Instances, password management, authentication, cloud directory, applications
- **App Configuration** - App Configuration instances
- **Activity Tracker** - Routes and targets
- **Cloud Shell** - Account settings
- **Placement Group** - Server placement groups

