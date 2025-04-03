--- 

title: "iManage Cloud Graph connector" 
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
description: "Set up the iManage Cloud Graph connector for Microsoft Search and Microsoft 365 Copilot" 
ms.date: 04/02/2025
---

# iManage Cloud Microsoft Graph connector (Preview)

The iManage Cloud Graph connector allows your organization to index content from iManage Cloud. After you configure the connector, end users can search for these content from iManage Cloud in Microsoft Copilot and from any Microsoft Search client.
 
This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors a iManage Cloud Graph connector.

>[!NOTE]
>The iManage Cloud connector is in private preview. If you wish to get access to try it, you need to enable [Targeted Release](/microsoft-365/admin/manage/release-options-in-office-365#set-up-the-release-option-in-the-admin-center) ring for your Admin account.

## Capabilities
- Index documents and emails from iManage Cloud with access control.
- Use [Semantic search in Copilot](semantic-index-for-copilot.md) to enable users to find relevant content based on keywords, personal preferences, and social connections.

## Limitations
- This Graph Connector is exclusively compatible with iManage Cloud (imanagecloud.com). iManage Work on-premises is not supported at this time. 
- Content marked as requiring HIPAA compliance will not be indexed. 

## Prerequisites
- You must be the **search admin** for your organization's Microsoft 365 tenant.
- **iManage Cloud instance URL**: You will need your organization's iManage Cloud instance URL, which is typically: [https://cloudimanage.com](https://cloudimanage.com/).
- **iManage Cloud NRTADMIN account**: To install the Microsoft iManage Cloud connector application in iManage Cloud, you need an iManage account with NRTADMIN permission.
- **iManage Cloud Help Center account**: To obtain the OAuth 2.0 Client ID and Client Secret, you need an active iManage Cloud Help Center account to register the application via iManage Support for your organization and get the OAuth 2.0 credentials.
## Get Started

### 1. Display name 
A display name is used to identify each reference in Copilot, helping users easily recognize the associated file or item. Display name also signifies trusted content.

### 2. iManage Cloud instance URL
The iManage Cloud instance URL is essential to correctly access and update data from, which is typically: [https://cloudimanage.com](https://cloudimanage.com/).
By the instance URL, the Graph Connector can reliably synchronize data changes and ensure accurate content delivery from iManage Cloud to connected Microsoft 365.

### 3. Authentication Type

**iManage Cloud OAuth**

We support the OAuth 2.0 authentication for iManage Cloud. To use the iManage Cloud OAuth for authentication, follow these steps.
#### Step 1: Install Microsoft iManage Cloud connector in iManage Cloud ####
Your organization's iManage Cloud administrator needs to install the **Microsoft - iManage Cloud Graph Connector** in iManage Control center with below recommended settings:


A iManage administrator needs to create an OAuth client in the [iManage App Registration portal](https://apps.iManage.com/apps). To learn more, see [Login with authorization_code flow](https://developer.iManage.com/iManagesoftware/reference/authorization-code-login) in the iManage documentation.

The following table provides the mandatory values for OAuth client creation:

Field | Description | Recommended Value
--- | --- | ---
Authentication Method | The OAuth 2 Authentication Method to authenticate and authorize users securely | OAuth2 - Authorization Code Flow (User Authentication)
Redirect URIs (redirect_uri) | The callback URL for Microsoft Graph connector | `https://gcs.office.com/v1.0/admin/oauth/callback`  
Scopes | The scopes to create a new version and a new client id and secret. | Below scopes are mandatory: iManage.user.view, iManage.configuration.view, iManage.reporting, iManage.library.view 
   
Enter the client ID (Unique identifier) and Secret to connect to your instance. After connecting, use a iManage administrator account credential to authenticate permission to crawl.

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
| Manage Properties | _To check default properties and their schema._ |

| Sync | Description |
|---|---|
| Incremental Crawl | _Frequency: Every 15 mins_ |
| Full Crawl | _Frequency: Every Day_ |

If you want to edit any of these values, you need to choose the "Custom Setup" option.

## Custom setup

Custom setup is for those admins who want to edit the default values for settings listed in the above table. Once you click on the **Custom Setup** option, you see three more tabs - **Users**, **Content**, and **Sync**.

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

Select time range: Select a time range for the content to be indexed. Only content with a last modified date and time within the selected range will be indexed. Choose an appropriate time range based on the volume of content to be indexed. Selecting "All time" may significantly impact your platform's performance if there is a large volume of content to be indexed.

**Manage properties**

Here, you can view available properties from your iManage Cloud, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label and add an alias to the property. Properties that are selected by default are listed below.

|Source property|Label|Description|Schema|
|---|---|---|---|
| AssignedToProfiles | | | Search |
| Content |  | | Search |
| CreatedAt | Created date time | Data and time that the item was created in the data source. | Query, Refine, Retrieve |
| CreatedBy | Created by | Name of the person who created the item in the data source. | Query, Retrieve, Search |
| Description | | | Query, Retrieve, Search |
| ExpiresAt | | | |
| Format | File extension | | Query, Refine, Retrieve |
| IconUrl | IconUrl | | Query, Retrieve, Search |
| Id | | | |
| ModifiedAt | Last modified date time | Date and time the item was last modified in the data source. | Query, Refine, Retrieve |
| ModifiedBy | Last modified by | Name of the person who most recently edited the item in the data source. | Query, Retrieve, Search |
| Name | Title | The title of the item that you want to be shown in Copilot and other search experiences. | Query, Retrieve, Search |
| Properties | | | Search |
| Repository | | | Query, Retrieve, Search |
| Size | | | |
| Status | | | |
| Type | | | |
| Url | url | The target URL of the item in the data source. | Query, Retrieve, Search |
| Version | | | |

### Sync

The refresh interval determines how often your data is synced between the data source and the iManage Cloud Microsoft Graph connector index. There are two types of refresh intervals - full crawl and incremental crawl. For more details, see [refresh settings](configure-connector.md#guidelines-for-sync-settings).

You can change the default values of the refresh interval from here if you want to.

## Troubleshooting
After publishing your connection, you can review the status under the **Data Sources** tab in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
