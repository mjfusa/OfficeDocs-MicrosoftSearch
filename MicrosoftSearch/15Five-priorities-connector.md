---

title: "15Five Priorities Microsoft Graph connector" 
ms.author: wangchen
author: wangchen
audience: Admin
ms.audience: Admin 
ms.topic: article 
ms.service: mssearch 
ms.localizationpriority: Medium 
search.appverid: 
- BFB160 
- MET150 
- MOE150 
description: "Set up the 15Five Priorities Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot" 
ms.date: 02/19/2025
---

# 15Five Priorities Microsoft Graph connector (preview)

With the  15Five Priorities Microsoft Graph connector, your organization in Microsoft 365 can index 15Five priority data, using Microsoft 365 Copilot and Microsoft Search. 

This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors 15Five Priorities Microsoft Graph connector. 

>[!NOTE]
>The 15Five Priorities Microsoft Graph connector is in preview. If you wish to get early access to try it, sign up using [this form](https://forms.office.com/r/JniPmK5bzm).

## Capabilities
- Access 15Five priorities using the power of semantic search
- Customize your crawl frequency
- Create workflows using this connection and plugins from Microsoft Copilot Studio



## Limitations

- Only the employee and their direct manager have access to the priority data using Microsoft 365 Copilot and Microsoft Search.



## Prerequisites

Before you create a 15Five Priorities Microsoft Graph connector, you must:

### 1. Setup a HR administrator in 15Five
Created a 15Five account with HR administrator permission.

### 2. **Create a company API key and get the access token**
Navigate to the Integrations admin setting page with the HR administrator account. Create a company API key and get the access token.



## Setup

### 1. Display name   
Choose a display name that helps users easily recognize associated file or item in a Copilot response.

### 2. **Instance URL**
The default 15Five instance URL is https://my.15five.com.

### 3. **Authentication type**
Select the available authentication type and enter the access token you obtained from your 15Five company API keys setting.

### 4. Rollout to a limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other search surfaces before expanding the rollout to a broader audience.



## Custom setup 

Custom setup is for those admins who want to edit the default values for settings. Once you click **Custom setup** , you should see three other tabs – Users, Content, and Sync. 

### Users 

**Access permissions**

Determine which users in your organization can access each item in Copilot or Search surfaces. Choose whether indexed data is visible to everyone in the organization or only to users who have access to them in the data source.  

### Content 

**Manage properties**

Here, you can add or remove available properties from your 15Five data source. Assign a schema to the property, change the semantic label, and add an alias to the property. Properties that are selected by default are:

|Source property|Label|Description|
|--- | ---- | --- |
|Text |  | The description of the priority. |
|Status |  | Status of the priority. |
|UserEmail |  | Email of the priority submitter. |
|ManagerEmail |  | Email of the manager of the submitter. |
|CreateTime | `createdDateTime` | The time at which the file was created. |
|UpdateTime	| `lastModifiedDateTime` | The last time the file was modified. |


### Sync 

You can configure full and incremental crawls based on the scheduling options present here. By default, incremental crawl is set for every 15 minutes, and full crawl is set for every day. If needed, you can adjust these schedules to fit your data refresh needs.



## Troubleshooting

### **Your security credentials have expired for this session. Please go back and sign in again with your App key and App secret.**
Credential info has expired. Please create a new key in 15Five integrations setting and copy the latest access token from the setting tab to authenticate.

### **Invalid Credentials detected. Please check the credential info and check the permission scopes of the 15Five App.**
Common credential error. Please go back to the 15Five integrations setting and check if the access token is correct.



## What's next

After publishing your connection, you can review the status under the **Data sources** tab in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have any other issues or want to provide feedback, reach out to us at [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
