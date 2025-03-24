--- 

title: "Miro Microsoft Graph connector (preview)" 
ms.author: anggao
author: ms-anggao
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
description: "Set up the Miro Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot." 
ms.date: 03/11/2025
---

# Miro Microsoft Graph connector (preview)

The Miro Microsoft Graph connector allows your organization to index boards from Miro. After you configure the connector, users can search for these boards from Miro in Microsoft 365 Copilot and from any Microsoft Search client.

This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors a Miro Microsoft Graph connector.

>[!NOTE]
>The Miro connector is in public preview. To get access to the connector, enable the [Targeted Release](/microsoft-365/admin/manage/release-options-in-office-365#set-up-the-release-option-in-the-admin-center) ring for your Admin account.

## Capabilities

- Access files in Copilot by using the power of Semantic search.
- Customize your crawl frequency.
- Create workflows by using this connection and actions from Microsoft Copilot Studio.

## Limitations

- Doesn't index attachments.
- Doesn't index comments and reply.

## Prerequisites

### 1. Create a Developer team for your Miro account

Create or use an existing Miro account to access Miro and click the [link](https://miro.com/app/dashboard/?createDevTeam=1) to create a Developer team for your active Miro account. If your organization is on an Enterprise plan, go to [Enterprise Developer teams](https://help.miro.com/hc/en-us/articles/4766759572114). For more information, see [Create a Developer team](https://developers.miro.com/docs/create-a-developer-team).

### 2. Create your app in Miro

Sign in to Miro and create a new app in [Your apps](https://miro.com/app/settings/user-profile/apps).

### 3. Add permissions to your app

Add the `boards:read Read boards you have access to` plan in the app you created in your app's configuration

### 4. Install your app and record credentials

Click **Install app and get OAuth token** and record the `Client ID` and `Client secret` from the app credentials.

## Get started

### 1. Display name

A display name is used to identify each citation in Copilot to help users easily recognize the associated file or item. The display name also signifies trusted content and is used as a [content source filter](/MicrosoftSearch/custom-filters#Content-source-filters). A default value is provided for this field; you can customize it to a name that users in your organization recognize.

### 2. Team ID

A Miro Team ID is an identifier for a specific team within the Miro platform. To find your Team ID, sign in to Miro in a browser, go to the settings of the team from your dashboard, and copy the ID.

>[!NOTE]
> You can only associate one team ID in the connection. If you have multiple team IDs in your Miro workspace, create a separate connection.

### 3. Authentication Type

**Miro OAuth**
Enter the Client ID and Client secret you obtained from your Miro app. For more information, see [Get started with OAuth 2.0 and Miro](https://developers.miro.com/docs/getting-started-with-oauth).

### 4. Roll out to limited audience

Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before you expand the rollout to a broader audience. For more information, see [Staged rollout for Microsoft Graph connectors](staged-rollout-for-graph-connectors.md).

Now you're ready to create the connection for Miro. Choose **Create** to publish your connection and index boards from your Miro account.

For other settings, like **Access permissions**, **Schema**, and **Crawl frequency**, default values are set based on what works best with Miro data.

| Users | Description |
|----|---|
| Access permissions | Only people with access to content in Data source. |
| Map identities | Data source identities mapped using Microsoft Entra IDs. |

| Content | Description |
|---|---|
| Manage properties | To check default properties and their schema. |

| Sync | Description |
|---|---|
| Full crawl | Frequency: Every day |

If you want to edit any of these values, choose the **Custom Setup** option.

## Custom setup

Custom setup is for admins who want to edit the default values for any settings. When you choose **Custom Setup**, you see three tabs: **Users**, **Content**, and **Sync**.

### Users

#### Access permissions

The Miro Microsoft Graph connector supports search permissions that are visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them.

#### Mapping identities

The default method for mapping your data source identities with Microsoft Entra ID is to verify that the email ID of Miro users is the same as the user principal name (UPN) or email of the users in Microsoft Entra. If the default mapping doesn't work for your organization, you can provide a custom mapping formula. For more information, see [Map your non-Azure AD Identities](map-non-aad.md).

To identify which option is best for your organization:

- Choose the **Microsoft Entra ID** option if the email ID of Miro users is the **same** as the users' UPN or email in Microsoft Entra ID.
- Choose the **Non-Microsoft Entra ID** option if the email ID of Miro users is **different** from the users' UPN and email in Microsoft Entra ID.

### Content

#### Manage properties

You can add or remove available properties from your Miro, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), and change the semantic label and add an alias to the property. The following table lists the properties that are selected by default.

|Source property|Label|Description|Schema|
|---|---|---|---|
|	Body	|	NA	|	NA	|	Search	|
|	CreatedAt	|	Created date time	|	Date and time that the item was created in the data source	|	Query, Retrieve	|
|	CreatedBy	|	Created by	|	The user who created the item 	|	Query, Retrieve, Search	|
|	Description	|	NA	|	NA	|	Query, Retrieve	|
|	Id	|	NA	|	NA	|	Query, Retrieve	|
|	ModifiedAt	|	Last modified date time	|	Date and time the item was last modified in the data source.	|	Query, Retrieve	|
|	ModifiedBy	|	Last modified by	|	The user who made the last modification 	|	Query, Retrieve, Search	|
|	Name	|	Title	|	The title of the item that you want shown in Copilot and other search experiences	|	Query, Retrieve, Search	|
|	Team	|	NA	|	NA	|	Query, Retrieve	|
|	ViewLink	|	url	|	The target URL of the item in the data source	|	Query, Retrieve	|

#### Preview data

Use the preview results button to verify the sample values of the selected properties and query filter.

### Sync

The refresh interval determines how often your data is synced between the data source and the Miro Microsoft Graph connector index. Only full crawl refresh intervals are supported. For more information, see [refresh settings](configure-connector.md#guidelines-for-sync-settings).

You can change the default values of the refresh interval.

## Troubleshooting

The following are common errors and how to resolve them.

**Required permission scopes are missing. Ensure the necessary scopes are selected in the Miro App.**

You don't have the required permission scopes. Make sure that you selected `boards:read
Read boards you have access to` in the permission field of your Apps configuration tab.

**OAuth 2.0 flow failed. Verify the credential information and make sure that the Miro App is configured with the correct settings.**

This is a common authentication error. Go back to the Miro app and verify that the OAuth2 in the setting tab is correctly configured.

**OAuth 2.0 flow failed. Confirm that the Miro user associated with this team access token holds the team admin role and is an active user.**

This is a common authentication error. Go back to the Miro app console and verify that the creator has an admin role and the account status is active.

**Your security credentials have expired for this session. Go back and sign in again with your App key and App secret.**

Your credential information expired. Refresh the Miro app and copy the latest Client ID and Client secret from the setting tab to authenticate.

**Invalid Credentials detected. Check the credential info and check the permission scopes of the Miro App.**

This is a common credential error. Go back to the Miro App and verify that the scopes in the permission tab are correctly configured.

## Next steps

After you publish your connection, you can review the status under the **Data Sources** tab in the [admin center](https://admin.microsoft.com). For more information, see [Manage your connector](manage-connector.md).

For help and support, see [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).