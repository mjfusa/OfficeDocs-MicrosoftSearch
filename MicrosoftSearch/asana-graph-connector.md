--- 
title: "Asana Microsoft Graph connector" 
ms.author:  kailiang
author: Kai-Cloud
manager:  
audience: Admin
ms.audience: Admin 
ms.topic: article 
ms.service: mssearch 
ms.localizationpriority: medium 
search.appverid: 
description: "Set up the Asana Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot" 
ms.date: 07/22/2021
---

# Asana Microsoft Graph connector

The Asana Microsoft Graph connector allows your organization to index Asana tasks. After you configure the connector and index content from the Asana workspaces, end users can search for those items in Microsoft Search and Microsoft 365 Copilot.

This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors an Asana Microsoft Graph connector.

## Capabilities
- Index tasks
- Enable your end users to ask questions related to project tracking and task infomration in Copilot.
   - Identify tasks that haven't been assigned yet across all my projects.
   - Check whether there are any overdue tasks in 'Client Presentation' project.
   - Summarize my tasks for the next two weeks.
- Use [Semantic search in Copilot](semantic-index-for-copilot.md) to enable users to find relevant content based on keywords, personal preferences, and social connections.

## Limitations
- The connector doesn't index comments.

## Prerequisites
- You must be the **search admin** for your organization's Microsoft 365 tenant.
- **Asana URL**: To connect to your Asana workspace, you need confirm the Asana URL. Normally, it should be 'https://app.asana.com'.
- **Asana Account**: To connect to Asana and allow Microsoft Graph Connector to update Asana tasks regularly, you need a service account with read permissions granted to the service account. The service account must have 'Admin' role.

## Get started

### 1. Display name 
A display name is used to identify each citation in Copilot, helping users easily recognize the associated file or item. Display name also signifies trusted content. The display name is also used as a [content source filter](/MicrosoftSearch/custom-filters#content-source-filters). A default value is present for this field, but you can customize it to a name that users in your organization recognize.

### 2. Asana URL
To connect to your Asana workspace, you need confirm the Asana URL. Normally, it should be 'https://app.asana.com'

### 3. Authentication type
**Asana OAuth**

To use the Asana OAuth for authentication, follow these steps.

An Asana admin needs to create an app in the [Asana developer console](https://app.asana.com/0/my-apps).

The following table provides guidance on how to fill out the OAuth client creation form:

Field | Description | Recommended Value
--- | --- | ---
App name | Unique value that identifies the application that you require OAuth access for. | Microsoft Search
Which best describes what your app will do? | Describe the purpose of the app | Tick 'Get data out of Asana to create reports'
Redirect URL | A required callback URL that the authorization server redirects to. | For **M365 Enterprise**: https://<span>gcs.office.</span>com/v1.0/admin/oauth/callback,</br> For **M365 Government**: https://<span>gcsgcc.office.<span>com/v1.0/admin/oauth/callback
Manage distribution | Choose workspaces to be distributed | Add specific workspaces that shall be accessed by the connector or select 'Any workspace'
   
Copy the client ID and client secret from the OAuth tab in your created Asana app and paste to the connector setup. Click Authorize, use the same Asana admin account credential to authenticate permission to crawl.
> [!NOTE]
>
> It is necessary to authorize access to the Asana app in a pop-up window. Ensure that your browser permits pop-up windows or locate the blocked pop-up window and grant access there.

### 4. Roll out to a limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience. To know more about limited rollout, [click here](staged-rollout-for-graph-connectors.md).

At this point, you're ready to create the connection for Asana. You can click on the "Create" button to publish your connection and index articles from your Asana account.

For other settings, like **Access permissions**, **Schema**, and **Crawl frequency**, we have default values based on what works best with Asana data.

| Users | Description |
|----|---|
| Access permissions | _Only people with access to content in Data source._ |
| Map Identities | _Data source identities mapped using Microsoft Entra IDs._ |

| Content | Description |
|---|---|
| Manage Properties | _To check default properties and their schema, see [content](#content)_ |

| Sync | Description |
|---|---|
| Incremental Crawl | _Frequency: Every 15 mins_ |
| Full Crawl | _Frequency: Every Day_ |

If you want to edit any of these values, you need to choose the "Custom Setup" option.

## Custom setup

Custom setup is for those admins who want to edit the default values for settings listed in the above table. Once you click on the "Custom Setup" option, you see three more tabs - Users, Content, and Sync.

### Users

[![Screenshot that shows Users tab where you can configure access permissions and user mapping rules.](media/asana-users-tab.png)](media/asana-users-tab.png#lightbox)

**Access permissions**

The Asana Microsoft Graph connector supports search permissions visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them. In Atlassian Asana, security permissions are defined using project permission schemes containing site-level groups and project roles. task-level security can also be defined using task-level permission schemes.

**Mapping identities**

The default method for mapping your data source identities with Microsoft Entra ID is by checking whether the email ID of Asana users is the same as the UserPrincipalName (UPN), or Mail of the users in Microsoft Entra. If you believe the default mapping wouldn't work for your organization, you can provide a custom mapping formula. To know more about, mapping Non-Microsoft Entra ID identities, see [Map your non-Azure AD Identities](map-non-aad.md).

To identify which option is suitable for your organization:

1. Choose the **Microsoft Entra ID** option if the Email ID of Asana users is the **same** as the UserPrincipalName (UPN) of users in Microsoft Entra ID.
2. Choose the **Non-Microsoft Entra ID** option if the Email ID of Asana users is **different** from the UserPrincipalName (UPN) and Email of users in Microsoft Entra ID.

### Content

[![Screenshot that shows Content tab where you can configure properties and schema.](media/asana-content-tab.png)](media/asana-content-tab.png#lightbox)

**Manage properties**

Here, you can add or remove available properties from your Asana, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label and add an alias to the property. Properties that are selected by default are listed below.

|Source property|Label|Description|Schema|
|---|---|---|---|
| Assignee | | The person who should complete this task | Query, Retrieve, Search |
| Completed | Content | The main body of the article|  Query, Retrieve |
| CompletedAt | | | Query, Retrieve |
| CreatedAt | Created date time | Date and time that the task was created | Query, Retrieve |
| CreateBy | Created by | | Query, Retrieve, Search |
| DueOn | | When this task should be completed | Query, Retrieve |
| Gid | | | Query, Retrieve |
| ModifiedAt | Last modified date time | | Query, Retrieve |
| Name | Title | | Query, Retrieve, Search |
| Notes |  | Description of the task | Search |
| ProjectIds | | | |
| ProjectNames | | | Query, Retrieve |
| Tags | | | Query, Retrieve |
| TaskUrl | url | | Query, Retrieve, Search |
| WorkspaceName | | | Query, Retrieve, Search |

**Preview data**

Use the preview results button to verify the sample values of the selected properties and query filter.

### Sync

[![Screenshot that shows Sync tab where you can configure crawl frequency.](media/asana-sync-tab.png)](media/asana-sync-tab.png#lightbox)

The refresh interval determines how often your data is synced between the data source and the Asana Microsoft Graph connector index. There are two types of refresh intervals - full crawl and incremental crawl. For more details, see [refresh settings](configure-connector.md#guidelines-for-sync-settings).

You can change the default values of the refresh interval from here if you want to.

## Troubleshooting
After publishing your connection, you can review the status under the **Data Sources** tab in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
