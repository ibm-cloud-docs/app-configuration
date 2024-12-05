---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-07"

keywords: app-configuration, app configuration, create a snapshot, snapshots, git configuration, gitops, git config

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Creating a snapshot
{: #ac-snapshots}

Snapshots are a way to capture the current configuration of your app or environment and sync the modified config set back to your config git repo. This can help you in versioning, application bootstrapping, rollback, troubleshooting, or audit {{site.data.keyword.appconfig_short}}.
{: shortdesc}

Every snapshot configuration will have the collection and environment id associated with it, along with this user
can provide their GitHub details where they would like to promote their configurations.

By default, **Snapshots** displays the list of snapshot in the current {{site.data.keyword.appconfig_short}} service instance along with **Name**, **Collection_id** associated, **Environment_id** associated, **Git_branch**, **Git_url**, **Git_file_path**, **Git_token**, **last_sync_time** and the date of creation of the snapshot, and the latest date it was updated.
{: note}

## Configure a snapshot
{: #ac-create-a-snapshot}

To create a snapshot, complete these steps:

1. From the {{site.data.keyword.appconfig_short}} console, click **Manage Snapshots** from the top menu bar.

   ![Manage snapshots](images/ac-manage-snapshots.png "Manage snapshots"){: caption="Manage snapshots in the current {{site.data.keyword.appconfig_short}} service instance" caption-side="bottom"}

1. Click **Manage Snapshots**. The side panel opens up where you will be seeing the **New +** button.

   ![Configure a snapshot](images/ac-configure-snapshots.png "Configure a snapshot"){: caption="{{site.data.keyword.appconfig_short}} service creating a new snapshot" caption-side="bottom"}

1. Click the **New +** button. You will see the page where you need to provide the snapshot details.

   ![Configure a new snapshot](images/ac-create-snapshots.png "Configure a new snapshot"){: caption="{{site.data.keyword.appconfig_short}} service configuring a new snapshot" caption-side="bottom"}

   - **Name** - name of the snapshot.
   - **Collection ID** - the collection identifier, you can select the value from the dropdown menu.
   - **Environment ID** - the environment identifier, you can select the value from the dropdown menu.
   - **Repository URL** - specify the GitHub URL, for example if you want the configuration to be written to organisation GitHub account then here is the URL `https://github.{{org_name}}.com/api/v3/repos/{{owner}}/{{repo_name}}` or if you want to write to your personal GitHub then the URL will be `https://api.github.com/repos/{{owner}}/{{repo_name}}`.
   - **Branch** - Add the branch name, to which you would like to write or update the config file.
   - **Folder path URL** - Provide the folder path to the file.
   - **File name** - provide the file name, we only allow `.json` or `.JSON` file extension.
   - **Git token** - provide the git token, this is the Personal access token this needs to be created with basic read, write and update permission. [How to create personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).

      Make sure you have selected the permissions as in Figure 4 when creating the **Git token**.
      {: note}

      ![Permissions to be selected during Git token creation](images/ac-snapshots-git-token.png "Permissions to be selected during Git token creation"){: caption="Permissions to be selected during Git token creation" caption-side="bottom"}

1. Click **Save**.

1. Once the snapshot is created, it will be listed in the **Manage snapshots** window.

   ![View configured snapshot](images/ac-list-snapshots.png "View configured snapshot"){: caption="{{site.data.keyword.appconfig_short}} service view configured snapshots" caption-side="bottom"}

## Create a GitHub snapshot
{: #ac-promote-a-snapshot}

To promote a snapshot, complete these steps:

1. First create the snapshot as suggested in the above steps.

1. Then you will see your configuration saved and displayed on the screen.

1. Click on the **Create snapshot**, if your configuration is correct then you will see the json file will be either updated if already exists, or it will be created if it does not exist.

   You can update the snapshot information using the API 'https://cloud.ibm.com/apidocs/app-configuration?code=go#update-gitconfig'.
   {: note}

## Restore a GitHub snapshot
{: #ac-restore-a-snapshot}

To restore a snapshot from GitHub, complete these steps:

1. From the {{site.data.keyword.appconfig_short}} console, click **Manage Snapshots** from the top menu bar.

   ![Manage snapshots](images/ac-restore-snapshots.png "Manage snapshots"){: caption="Manage snapshots in the current {{site.data.keyword.appconfig_short}} service instance" caption-side="bottom"}

1. Click **Manage Snapshots**. The side panel opens up with existing snapshots.

1. Click **Restore Snapshot** to restore the required configuration to your {{site.data.keyword.appconfig_short}} instance.

Only the lastest snapshot stored in GitHub will be restored. Commit based snapshot restore not supported.
{: note}

## Snapshot - overflow menu
{: #snapshot-overflow-menu}

The overflow menu for each of the snapshot (three vertical dots) consist of **Delete** operation.

When **Delete** option is selected, a confirmation window is displayed to seek confirmation to delete the selected snapshot. Delete option permanently deletes the snapshot, this action cannot be undone.
{: note}
