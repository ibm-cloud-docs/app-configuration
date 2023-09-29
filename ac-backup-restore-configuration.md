---

copyright:
  years: 2021, 2022, 2023
lastupdated: "2023-09-28"

keywords: app-configuration, app configuration, set up environments feature flags and properties, feature flags, properties, environments, backup, restore

subcollection: app-configuration

---

{{site.data.keyword.attribute-definition-list}}

# Backup and Restore instance configuration
{: #ac-backup-restore-configuration}

The ability to import and export data is essential for managing and maintaining instance setups. The usage of these functionalities makes it easier to perform procedures like system replication, backup, and version control by allowing users to smoothly move configuration settings between instances. Additionally, this config api offers to integrate seamlessly with version control systems like Git, allowing users to capture configuration snapshots and commit them to a repository. This integration not only provides a historical record of configuration changes but also facilitates easy rollback to previous configurations when needed. Users can confidently experiment with different configurations, knowing they can always revert to a known working state by restoring configurations from their Git repository, ensuring robust configuration management and system stability.
{: shortdesc}

## Import

Users can import whole configuration data into a App configuration instance to ensure accuracy and consistency when configuring complicated systems.

## Export

In contrast, export functionality gives users the ability to extract current whole configurations for a variety of reasons, including sharing settings with team members, making backups, or moving settings to a new instances. 

## Promote snapshot

Users can promote a specific configuration, which is based on the environment and collection id, to Git. For more information, see [Promote Snapshot](/docs/app-configuration?topic=app-configuration-ac-snapshots#ac-promote-a-snapshot)


## Restore snapshot

Users are able to restore the particular configuration from Git. For more information, see [Restore Snapshot](/docs/app-configuration?topic=app-configuration-ac-snapshots#ac-restore-a-snapshot)