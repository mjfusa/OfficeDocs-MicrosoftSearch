--- 

title: "iManage Cloud Microsoft Graph connector" 
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
description: "Set up the iManage Cloud Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot" 
ms.date: 04/02/2025
---

# iManage Cloud Microsoft Graph connector (Preview)

The iManage Cloud Graph Connector allows your organization to index content from iManage Cloud. After you configure the connector, end users can search for this content from iManage Cloud in Microsoft Copilot and from any Microsoft Search client.
 
This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors a iManage Cloud Graph Connector.

>[!NOTE]
>The iManage Cloud connector is in private preview for invited customers only. If you are invited and wish to get access to try it, you need to enable [Targeted Release](/microsoft-365/admin/manage/release-options-in-office-365#set-up-the-release-option-in-the-admin-center) ring for your Admin account.

## Capabilities
- **Indexing with Access Control**: Index documents and emails from iManage Cloud while maintaining access control.
- **Selective Content Indexing**: Use content filters to selectively index content based on criteria such as time range filter and library filter.
- **Sensitive Content Exclusion**: By default, content marked as HIPAA compliant are not indexed to ensure sensitive information is excluded.
- **[Semantic search in Copilot](semantic-index-for-copilot.md)**: Enable users to find relevant content based on keywords, personal preferences, and social connections

## Limitations
- **Compatibility**: This Connector is exclusively compatible with iManage multi-tenant Cloud (also known as iManage Work at cloudimanage.com).
- **Unsupported Environments**: iManage Work on-premises or iManage single-tenant Cloud hosted in iManage Cloud at imanage.work and other domains aren't supported at this time.
- **HIPAA Compliance**: iManage content marked as requiring HIPAA compliance will not be indexed.

## Prerequisites
- You must be the **search admin** for your organization's Microsoft 365 tenant.
- **iManage Cloud instance URL**: You need your organization's iManage Cloud instance URL, which is typically: [https://cloudimanage.com](https://cloudimanage.com/).
- **iManage Cloud NRTADMIN account**: To install the Microsoft iManage Cloud connector application in iManage Cloud, you need an iManage account with NRTADMIN permission to complete the OAuth 2.0 Authentication in Microsoft Admin Center.
- **OAuth Client_ID and Client_Secret**: Obtain the OAuth Client_ID and Client_Secret from iManage support before setting up the iManage Cloud connection in the Microsoft Admin Center.
- **Add and authorize Microsoft iManage Cloud application**: You need to add and authorize the Microsoft iManage Cloud application in the iManage Cloud Control Center.

### 1. Display name 
A display name is used to identify each reference in Copilot, helping users easily recognize the associated file or item. Display name also signifies trusted content.

### 2. iManage Cloud instance URL
The iManage Cloud instance URL is essential to correctly access and update data from, which is typically: [https://cloudimanage.com](https://cloudimanage.com/).

### 3. Authentication Type

**iManage Cloud OAuth 2.0**

We support OAuth 2.0 authentication for iManage Cloud. The connector is registered as an application titled **Microsoft - iManage Cloud Graph Connector**, which you can find on the iManage Cloud application page. To enable this application for your organization, follow these steps before setting up the iManage Cloud connection in [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal#/MicrosoftSearch/connectors).

#### Step 1: Add Microsoft iManage Cloud connector application ####
A new application registered and authorized for your iManage Cloud environment isn't enabled by default. Apps may be enabled in iManage Control Center by a user assigned to a Global Management role that has the App Management privilege.
You need to add the **Microsoft - iManage Cloud Graph Connector** in iManage Control center for your environment with below recommended values. [Learn more](https://docs.imanage.com/cloud/cc-help/en-US/Adding_an_application.html)

Area  |  Field | Recommended Value
--- | --- | ---
Status | Status | Enabled
Authentication | Allow Refresh Token | Yes
Authentication | Refresh Token Expiry | 365 days
Authentication | Access Token Expiry | 5,000 mins
Security | Allow access to | All Users

#### Step 2: Contact iManage support for OAuth credentials ####
Create a ticket to iManage support to get your Client_id and Client_secret for this iManage application to set up the iManage Cloud connection in Microsoft 365 admin center.
   
Enter the client ID (Unique identifier) and Secret to connect to your instance. After connecting, use an iManage NRTADMIN account credential to authenticate permission to crawl.

### 4. Roll out to limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience. To know more about limited rollout, [click here](staged-rollout-for-graph-connectors.md).

At this point, you're ready to create the connection for iManage Cloud. You can click on the "Create" button to publish your connection and index content from your iManage account.

For other settings, like **Access permissions**, **Schema**, and **Crawl frequency**, we have default values based on what works best with iManage data.


| Users | Description |
|----|---|
| Access permissions | _Only people with access to content in Data source._ |
| Map Identities | _Data source identities mapped using Microsoft Entra IDs._ |

| Content | Description |
|---|---|
| Select the libraries | All |
| Select Time range | _Last half a year_ |
| Manage Properties | _29 default content properties_ |

| Sync | Description |
|---|---|
| Incremental Crawl | _Frequency: Every 15 mins_ |
| Full Crawl | _Frequency: Every Day_ |

If you want to edit any of these values, you need to choose the "Custom Setup" option.

## Custom setup

Custom setup is for those admins who want to edit the default values for settings. Once you click on the **Custom Setup** option, you see three more tabs - **Users**, **Content**, and **Sync**.

### Users

**Access permissions**

The iManage Cloud Microsoft Graph connector supports search permissions visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them.

**Mapping identities**

The default method for mapping your data source identities with Microsoft Entra ID is by checking whether the email ID of iManage users is the same as the UserPrincipalName (UPN), or Mail of the users in Microsoft Entra. If you believe the default mapping wouldn't work for your organization, you can provide a custom mapping formula. To learn more about mapping Non-Microsoft Entra ID identities, see [Map your non-Azure AD Identities](map-non-aad.md).

To identify which option is suitable for your organization:

1. Choose the **Microsoft Entra ID** option if the Email ID of iManage users is the **same** as the UserPrincipalName (UPN) or email of users in Microsoft Entra ID.
2. Choose the **Non-Microsoft Entra ID** option if the Email ID of iManage users is **different** from the UserPrincipalName (UPN) and Email of users in Microsoft Entra ID.

### Content

**Content filter**
To optimize the indexing process, consider setting up multiple connections or utilizing content filters to reduce the number of items indexed per connection if the content exceeds the [connection limits](/graph/connecting-external-content-api-limits)

**Select the libraries**: Choose the specific libraries for the content to be indexed. Only the content within these selected libraries are indexed.

**Select time range**: Define a time range for the content to be indexed. Only content with a last modified date and time within the specified range to be indexed. Select an appropriate time range based on the volume of content to be indexed. 

>[!CAUTION]
> Selecting "All time" may significantly impact your platform's performance if there's a large volume of content to be indexed.

>[!TIP]
> If you have a substantial amount of content stored in your iManage libraries that needs to be indexed with this connector, we strongly recommend creating multiple connections. Each connection should cover only a small portion of the content stored in the iManage Cloud, with different full crawl starting times. This approach helps balance content freshness and performance. For example, each connection should index content less than 1-5 million items and have a full crawl starting time different from other connections.


**Manage properties**

Here, you can view available properties from your iManage Cloud. Assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label and add an alias to the property. Properties that are selected by default are listed below.

|Source property|Label|Description|Schema|
|---|---|---|---|
| Author             | Created by              | The person who created the content | Retrieve, Search       |
| CC                 |                         | Carbon copy recipients  | Query, Retrieve        |
| CoAuthors          |                         | Other authors of the content |                        |
| Authors            |                         | The main authors of the content | Retrieve, Search       |
| Comment            |                         | Comments associated with the content | Retrieve, Search       |
| Content            |                         | The main body of the content | Search                 |
| ConversationName   |                         | The name of the conversation | Retrieve, Search       |
| CreateDate         | Created date time       | The date and time when the content was created | Query, Retrieve        |
| CustomProperties   |                         | Custom properties associated with the content | Query, Retrieve        |
| DocumentNumber     |                         | The document number     | Query, Retrieve        |
| EditDate           | Last modified date time | The date and time when the content was last modified | Query, Retrieve        |
| Extension          | File extension          | The file extension       | Query, Retrieve        |
| FileCreateDate     |                         | The date and time when the file was created | Query, Retrieve        |
| FileEditDate       |                         | The date and time when the file was last edited | Query, Retrieve        |
| From               |                         | The sender of the content | Retrieve, Search       |
| HasAttachment      |                         | Indicates if the content has an attachment | Retrieve               |
| ID                |                         | The unique identifier of the content | Query, Retrieve        |
| LastUser           | Last modified by        | The last user who modified the content | Query, Retrieve, Search|
| Library            |                         | The library where the content is stored | Query, Retrieve        |
| Name               | File name               | The name of the file    | Retrieve, Search       |
| ReceivedDate       |                         | The date and time when the content was received | Query, Retrieve        |
| RelatedDocuments   |                         | Documents related to the content | Retrieve, Search       |
| SentDate           |                         | The date and time when the content was sent | Query, Retrieve        |
| Subject            |                         | The subject of the content | Retrieve, Search       |
| Title              | Title                   | The title of the content | Retrieve, Search       |
| To                 |                         | The recipients of the content | Retrieve, Search       |
| Url                | url                     | The URL of the content  | Retrieve, Search       |
| Version            |                         | The version of the content | Query, Retrieve        |
| WSType             |                         | The workspace type      | Query, Retrieve        |
| WorkspaceName      |                         | The name of the workspace | Query, Retrieve        |

### Sync

The refresh interval determines how often your data is synced between the data source and the iManage Cloud Microsoft Graph connector index. There are two types of refresh intervals - full crawl and incremental crawl. For more information, see [refresh settings](configure-connector.md#guidelines-for-sync-settings).

You can change the default values of the refresh interval from here if you want to.

>[!TIP]
> If you have a substantial amount of content stored in your iManage libraries that needs to be indexed with this connector, we strongly recommend creating multiple connections. Each connection should cover only a small portion of the content stored in the iManage Cloud, with different full crawl starting times. This approach helps balance content freshness and performance. For example, each connection should index content less than 1-5 million items and have a full crawl starting time different from other connections.

### Connection description
Upon creating the connection, navigate to the Success page. Here, you can click the **Auto Suggestion** button to use the default Connection description. Alternatively, you may create a custom Connection description to help Copilot better understand the indexed content and enhance the end user prompts when referencing content from this connection for your organization.

## Troubleshooting
After publishing your connection, you can review the status under the **Data Sources** tab in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
