---

copyright:
years: 2020, 2022
lastupdated: "2022-06-05"

keywords: app-configuration, app configuration, create a snapshot, snapshots, git configuration, gitops, git config

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Snapshots
{: #ac-snapshots}

Snapshots are a way to capture the current configuration of my app or environment and sync the modified config set 
back to my config git repo. This can help us in rollback. troubleshooting, or 
audit. {{site.data.keyword.appconfig_short}}
Every snapshot configuration will have the collection and environment id associated with it, along with this user 
can provide their git hub details where they would like to promote their configurations.  
{: shortdesc}


By default, **Snapshots** displays the list of snapshot in the current {{site.data.keyword.appconfig_short}} service 
instance along with **Name**, **Collection_id** associated, **Environment_id** associated, **Git_branch**, **Git_url** 
**Git_file_path**, **Git_token**, **last_sync_time** and the date of creation of 
the snapshot, and the latest date it was updated.
{: note}

## Create a snapshot
{: #ac-create-a-snapshot}

To create a snapshot, complete these steps:

1. From the {{site.data.keyword.appconfig_short}} console, click on **Manage Snaphots** from the top menu bar.

   ![List of snapshots]( "List of snapshots in the current {{site.data.keyword.
   appconfig_short}} service instance"){: caption="Figure 6. List of snapshots in the current {{site.data.keyword.
   appconfig_short}} service instance." caption-side="bottom"}

1. Click **Manage Snaphots**. The side panel opens with fields for creating a new snapshots.

   ![Create a snapshot]( "Creating a snapshot"){: caption="Figure 7. {{site.data.
   keyword.appconfig_short}} service creating a new snapshot" caption-side="bottom"}

1. Provide the snapshot details:
    - **Name** - name of the snapshot.
    - **Collection ID** - the collection identifier, you can select the value from the dropdown menu.
    - **Environment ID** - the environment identifier, you can select the value from the dropdown menu.   
    - **Repository URL** - specify the Git hub URL, for example if you want the configuration to be written to 
    organisation git hub account then here is the URL `https://api.github.{{org_name}}.com/repos/{{owner}}/{
    {repo_name}}` or if you want to write to your personal git hub then the URL will be `https://api.github.
    com/repos/{{owner}}/{{repo_name}}` 
    - **Branch** - Add the branch name, to which you would like to write or update the config file.
    - **Folder path URL** - Provide the folder path to the file
    - **File name** - provide the file name, we only allow `.json` or `.JSON` file extension
    - **Git token** - provide the git token, this is the Personal access token this needs to be created with basic 
    read, write and update permission.
    [How to create personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).
1. Click **Save**.


## Snapshot - overflow menu
{: #snapshot-overflow-menu}

The overflow menu for each of the snapshot (three vertical dots) consist of **Delete** operation.

![Overflow menu for a snapshot]( "Overflow menu for a snapshot"){: 
caption="Figure 8. Overflow menu for a snapshot" caption-side="bottom"}

* When **Delete** option is selected, a confirmation window is displayed to seek confirmation to delete the selected 
snapshot. Delete option permanently deletes the snapshot, this action cannot be undone.

{: note}

## Promote a snapshot
{: #ac-promote-a-snapshot}

To promote a snapshot, complete these steps:

1. First create the snapshot as suggested in the above steps.
2. Then you will see your configuration saved and displayed on the screen.
3. Click on the **Create snapshot**, if your configuration is correct then you will see the json file will be either 
updated if already exists, or it will be created if it does not exist. 
