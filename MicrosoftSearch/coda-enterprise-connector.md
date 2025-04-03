--- 

title: "Coda Enterprise Graph Connector" 
ms.author: depang
author: dennypanggh
manager: jecui
audience: Admin
ms.audience: Admin 
ms.topic: article 
ms.service: mssearch 
ms.localizationpriority: Medium 
search.appverid: 
- BFB160 
- MET150 
- MOE150 
description: "Set up the Coda Enterprise Graph Connector for Microsoft Search and Microsoft 365 Copilot" 
ms.date: 04/03/2025
---

# Coda Enterprise Graph connector (Preview)

The Coda Enterprise Graph Connector allows your organization to index documents and pages from Coda. After you configure the connector, end users can search for these content from Coda in Microsoft Copilot and from any Microsoft Search client.
 
This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors a Coda Enterprise Graph Connector.

>[!NOTE]
>The Coda Enterprise connector is in public preview. If you wish to get access to try it, you need to enable [Targeted Release](/microsoft-365/admin/manage/release-options-in-office-365#set-up-the-release-option-in-the-admin-center) ring for your Admin account.

## Capabilities
- **Indexing with Access Control**: Index documents and emails from Coda Enterprise instance while maintaining access control.
- **Selective Content Indexing**: Use content filters to selectively index content based on criteria such as time range filter.
- **[Semantic search in Copilot](semantic-index-for-copilot.md)**: Enable users to find relevant content based on keywords, personal preferences, and social connections

## Limitations
- **Supported Edition**: This Graph Connector is exclusively compatible with Coda Enterprise edition. 
- **Unsupported Edition**: Coda Free, Pro and Team Edition are not supported now due to Coda API restrictions on those editions.

## Prerequisites
- You must be the **search admin** for your organization's Microsoft 365 tenant.
- **Coda Org Administrator account**: To setup the Microsoft Coda Enterprise connector, you need an Coda Org administrator account to obtain the API Token to index content of your organization.
- **API Key**: Coda Enterprise supports API token authentication. The Coda API token can be obtained from the **Account settings** page of the Coda Org administrator.

### 1. Display name 
A display name is used to identify each reference in Copilot, helping users easily recognize the associated file or item. Display name also signifies trusted content.

### 2. Coda Enterprise instance Organization ID
The Coda Enterprise Organization ID is required to setup the connection, which usually follows this format, org-AbCDeFGHIj, and can be found in the page URL of Coda admin settings page such as `https://coda.io/organizations/org-AbCDeFGHIj/about`

### 3. Authentication Type

**Coda API Key**

To connect to the Coda Enterprise instance and allow Microsoft Graph Connector to index the Coda documents and pages regularly, you need to create a Coda Enterprise API token from the Coda Org Admin account.

Navigate to **Account settings** -> **API Settings** page of a Coda Org Admin account, Click **Generate API Token** to generate a new token using the default values below:
Field | Default Value
--- | ---
Type of restriction | Doc or table
Type of access | Read and write
Doc or table to grant access to | `not required, leave it to empty`

### 4. Roll out to limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience. To know more about limited rollout, [click here](staged-rollout-for-graph-connectors.md).

At this point, you're ready to create the connection for Coda. You can click on the "Create" button to publish your connection and index content from your Coda account.

For other settings, like **Access permissions**, **Schema**, and **Crawl frequency**, we have default values based on what works best with Coda data.


| Users | Description |
|----|---|
| Access permissions | _Only people with access to content in Data source._ |
| Map Identities | _Data source identities mapped using Microsoft Entra IDs._ |

| Content | Description |
|---|---|
| Select time range | _Last 1 year_ |
| Manage Properties | _12 default properties and their schema._ |

| Sync | Description |
|---|---|
| Incremental Crawl | _Frequency: Every 15 mins_ |
| Full Crawl | _Frequency: Every Day_ |

If you want to edit any of these values, you need to choose the "Custom Setup" option.

## Custom setup

Custom setup is for those admins who want to edit the default values for settings listed in the above table. Once you click on the **Custom Setup** option, you see three more tabs - **Users**, **Data**, and **Crawl**.

### Users

**Access permissions**

The Coda Enterprise Graph connector supports search permissions visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them.

**Mapping identities**

The default method for mapping your data source identities with Microsoft Entra ID is by checking whether the email ID of Coda users is the same as the UserPrincipalName (UPN), or Mail of the users in Microsoft Entra. If you believe the default mapping wouldn't work for your organization, you can provide a custom mapping formula. To learn more about mapping Non-Microsoft Entra ID identities, see [Map your non-Azure AD Identities](map-non-aad.md).

To identify which option is suitable for your organization:

1. Choose the **Microsoft Entra ID** option if the Email ID of Coda users is the **same** as the UserPrincipalName (UPN) or email of users in Microsoft Entra ID.
2. Choose the **Non-Microsoft Entra ID** option if the Email ID of Coda users is **different** from the UserPrincipalName (UPN) and Email of users in Microsoft Entra ID.

### Data

**Content filter**
Currently, Coda API limits are attached to a user/IP. To optimize the indexing performance, consider setting up multiple connections or utilizing content filter to reduce the number of items indexed per connection. 

**Select time range**: Define a time range for the content to be indexed. Only content with a last modified date and time within the specified range will be indexed. Select an appropriate time range based on the volume of content to be indexed. 

>[!CAUTION]
> Selecting "All time" may significantly impact your platform's performance if there is a large volume of content to be indexed.

**Manage properties**

Here, you can view available properties from your Coda, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label and add an alias to the property. Properties that are selected by default are listed below.

| Properties   | Semantic Label          | Schema                     | Description                                      |
|--------------|-------------------------|----------------------------|--------------------------------------------------|
| BrowserLink  | url                     | Retrieve                   | The URL link to the document or page             |
| Content      | CONTENT                 | Search                     | The main content of the document                 |
| CreatedAt    | Created date time       | Query, Retrieve            | The date and time when the document was created  |
| FolderId     | Query                   |                            | The unique identifier for the folder             |
| FolderName   | Query, Retrieve, Search |                            | The name of the folder                           |
| Id           | Query, Retrieve         |                            | The unique identifier for the document           |
| Name         | Title                   | Query, Retrieve, Search    | The title or name of the document                |
| Owner        | Query, Retrieve, Search |                            | The owner of the document                        |
| OwnerName    | Created by              | Query, Retrieve, Search    | The name of the person who created the document  |
| UpdatedAt    | Last modified date time | Query, Retrieve            | The date and time when the document was last modified |
| WorkspaceId  | Query                   |                            | The unique identifier for the workspace          |
| WorkspaceName| Query, Retrieve, Search |                            | The name of the workspace                        |

### Crawl

The refresh interval determines how often your data is synced between the data source and the Coda Microsoft Graph connector index. There are two types of refresh intervals - full crawl and incremental crawl. For more details, see [refresh settings](configure-connector.md#guidelines-for-sync-settings).

You can change the default values of the refresh interval from here if you want to.

>[!TIP]
> If you have a substantial amount of content stored in your Coda Enterprise instance that needs to be indexed with this connector, we strongly recommend you setup an approperiate crawl frequency to balance between content freshness in Copilot and the Coda Enterprise instance performance. Also, you can contact Coda support if any performance issues introduced by Coda API rate limits.

## Troubleshooting
After publishing your connection, you can review the status under the **Data Sources** tab in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
