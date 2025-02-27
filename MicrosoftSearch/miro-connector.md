--- 

title: "Miro Graph connector" 
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
description: "Set up the Miro Graph connector for Microsoft Search and Microsoft 365 Copilot" 
ms.date: 02/27/2025
---

# Miro Microsoft Graph connector (Preview)

The Miro Graph connector allows your organization to index boards from Miro. After you configure the connector, end users can search for these boards from Miro in Microsoft Copilot and from any Microsoft Search client.

This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors a Miro Graph connector.

>[!NOTE]
>The Miro connector is in public preview. If you wish to get access to try it, you need to enable [Targeted Release](/microsoft-365/admin/manage/release-options-in-office-365#set-up-the-release-option-in-the-admin-center) ring for your Admin account.

## Capabilities
- Access files in Copilot using the power of Semantic search
- Retain ACLs defined by your organization
- Customize your crawl frequency
- Create workflows using this connection and plugins from Microsoft Copilot Studio

## Limitations
- Doesn't index attachments
- Doesn't index comments and reply

## Prerequisites
### 1.	Create a Developer team for your Miro account
Create or use an existing Miro account to access Miro and click the [link](https://miro.com/app/dashboard/?createDevTeam=1) to create a Developer team for your currently active Miro account. If your organization is on an Enterprise plan, go to the [Enterprise Developer teams](https://help.miro.com/hc/en-us/articles/4766759572114). [Learn more](https://developers.miro.com/docs/create-a-developer-team)

### 2.	Create your app in Miro
Sign in to Miro and create a new app in the [Your apps](https://miro.com/app/settings/user-profile/apps). 

### 3.	Add permissions to your app
Add the `boards:read Read boards you have access to` plan in the app you created in app’s configuration

### 4.	Install your app and record credentials
Click “Install app and get OAuth token”and record the `Client ID` and `Client secret` from the App Credentials


## Get Started

### 1. Display name 
A display name is used to identify each citation in Copilot, helping users easily recognize the associated file or item. Display name also signifies trusted content. Display name is also used as a [content source filter](/MicrosoftSearch/custom-filters#Content-source-filters). A default value is present for this field, but you can customize it to a name that users in your organization recognize.

### 2. Team ID
A Miro Team ID is an identifier for a specific team within the Miro platform. To find your Team ID, log into Miro in a browser, go to the settings of the team from your dashboard, and you will be able to copy the ID
>[!NOTE]
> You can only associate one team ID in the connection. If you have multiple team id in your Miro workspace, please create seperated connection.

### 3. Authentication Type

**Miro OAuth**
Enter the Client ID and Client secret you obtained from your Miro app. [learn more](https://developers.miro.com/docs/getting-started-with-oauth)

### 4. Roll out to limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience. To know more about limited rollout, [click here](staged-rollout-for-graph-connectors.md).

At this point, you're ready to create the connection for Miro. You can click on the "Create" button to publish your connection and index boards from your Miro account.

For other settings, like **Access permissions**, **Schema**, and **Crawl frequency**, we have default values based on what works best with Miro data.

| Users | Description |
|----|---|
| Access permissions | _Only people with access to content in Data source._ |
| Map Identities | _Data source identities mapped using Microsoft Entra IDs._ |

| Content | Description |
|---|---|
| Manage Properties | _To check default properties and their schema. |

| Sync | Description |
|---|---|
| Full Crawl | _Frequency: Every Day_ |

If you want to edit any of these values, you need to choose the "Custom Setup" option.

## Custom setup

Custom setup is for those admins who want to edit the default values for settings listed in the above table. Once you click on the **Custom Setup** option, you see three more tabs - **Users**, **Content**, and **Sync**.

### Users

**Access permissions**

The Miro Microsoft Graph connector supports search permissions visible to **Everyone** or **Only people with access to this data source**. If you choose **Everyone**, indexed data appears in the search results for all users. If you choose **Only people with access to this data source**, indexed data appears in the search results for users who have access to them.

**Mapping identities**

The default method for mapping your data source identities with Microsoft Entra ID is by checking whether the email ID of Miro users is the same as the UserPrincipalName (UPN), or Mail of the users in Microsoft Entra. If you believe the default mapping wouldn't work for your organization, you can provide a custom mapping formula. To know more about, mapping Non-Microsoft Entra ID identities, see [Map your non-Azure AD Identities](map-non-aad.md).

To identify which option is suitable for your organization:

1. Choose the **Microsoft Entra ID** option if the Email ID of Miro users is the **same** as the UserPrincipalName (UPN) or email of users in Microsoft Entra ID.
2. Choose the **Non-Microsoft Entra ID** option if the Email ID of Miro users is **different** from the UserPrincipalName (UPN) and Email of users in Microsoft Entra ID.

### Content

**Manage properties**

Here, you can add or remove available properties from your Miro, assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label and add an alias to the property. Properties that are selected by default are listed below.

|Source property|Label|Description|Schema|
|---|---|---|---|
|	Body	|		|		|	Search	|
|	CreatedAt	|	Created date time	|	Date and time that the item was created in the data source	|	Query, Retrieve	|
|	CreatedBy	|	Created by	|	The user who created the item 	|	Query, Retrieve, Search	|
|	Description	|		|		|	Query, Retrieve	|
|	Id	|		|		|	Query, Retrieve	|
|	ModifiedAt	|	Last modified date time	|	Date and time the item was last modified in the data source.	|	Query, Retrieve	|
|	ModifiedBy	|	Last modified by	|	The user who made the last modification 	|	Query, Retrieve, Search	|
|	Name	|	Title	|	The title of the item that you want shown in Copilot and other search experiences	|	Query, Retrieve, Search	|
|	Team	|		|		|	Query, Retrieve	|
|	ViewLink	|	url	|	The target URL of the item in the data source	|	Query, Retrieve	|


**Preview data**

Use the preview results button to verify the sample values of the selected properties and query filter.

### Sync

The refresh interval determines how often your data is synced between the data source and the Miro Microsoft Graph connector index. Only full crawl refresh intervals is supported in Miro Graph Connector.For more details, see [refresh settings](configure-connector.md#guidelines-for-sync-settings).

You can change the default values of the refresh interval from here if you want to.

## Troubleshooting
### 1. Required permission scopes are missing. Please ensure the necessary scopes are selected in the Miro App.
Lack of the required permission scopes, please make sure you have selected `boards:read
Read boards you have access to` in the permssion field of your Apps configuration tab.

### 2. OAuth 2.0 flow failed. Please verify the credential information and ensure the Miro App is configured with the correct settings.
Common authentication error. Please go back to the Miro app  and check if the OAuth2 in the setting tab is correctly configured.

### 3. OAuth 2.0 flow failed. Please confirm that the Miro user associated with this team access token holds the team admin role and is an active user.
Common authentication error. Please go back to the Miro app console and check if the creator has an admin role and the account status is active.

### 4. Your security credentials have expired for this session. Please go back and sign in again with your App key and App secret.
Credential info has expired. Please refresh the Miro app  and copy the latest Client ID and Client secret from the setting tab to authenticate.

### 5. Invalid Credentials detected. Please check the credential info and check the permission scopes of the Miro App.
Common credential error. Please go back to the Miro App and check if the scopes in the permission tab are correctly configured.

