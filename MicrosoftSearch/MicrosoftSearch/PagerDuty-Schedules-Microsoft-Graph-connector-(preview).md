---

title: "PagerDuty Schedules Microsoft Graph connector (preview)" 
ms.author: wangchen
author: wangchen
manager: zezhangzhao
audience: Admin
ms.audience: Admin 
ms.topic: article 
ms.service: mssearch 
ms.localizationpriority: Medium 
search.appverid: 
- BFB160 
- MET150 
- MOE150 
description: "Set up the PagerDuty Schedules Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot." 
ms.date: 03/27/2025
---

# PagerDuty Schedules Microsoft Graph connector (preview)

The PagerDuty Schedules Microsoft Graph connector enables your organization to index PagerDuty schedule data to make it available to Microsoft 365 Copilot and Microsoft Search. 

This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors the PagerDuty Schedules Microsoft Graph connector. 

> [!NOTE]
> The Microsoft Graph PagerDuty Schedules connector is in preview. To request early access, submit the following [request form](https://forms.office.com/r/JniPmK5bzm).

## Capabilities

- Access PagerDuty schedules in Copilot using the power of Semantic search.

- Retain ACLs defined by your organization.

- Customize your crawl frequency.

- Create workflows using this connection and plugins from Microsoft Copilot Studio.

## Limitations

- When Advanced Permissions is enabled in PagerDuty, only members of the teams linked to a specific schedule can access and search for that schedule in Microsoft Search and Microsoft 365 Copilot.

## Prerequisites

Before you create a Microsoft Graph PagerDuty Schedules connector, complete the following steps:

1. Created a PagerDuty account with administrator permission in PagerDuty application.
2. Add a new app in PagerDuty with OAuth 2.0 functionality enabled. See [OAuth Functionality](https://developer.pagerduty.com/docs/oauth-functionality) and [Register an App](https://developer.pagerduty.com/docs/register-an-app) for more information.
3. Select ‘Scoped OAuth’ in PagerDuty new app registration setting page.
4. Use the following links for the field ‘Redirect URL’ in PagerDuty new app registration setting page.
   
   ·    For M365 Enterprise, copy and paste this URL 
   https://gcs.office.com/v1.0/admin/oauth/callback
   
   ·    For M365 Government, copy and paste this URL
   https://gcsgcc.office.com/v1.0/admin/oauth/callback

7. Select the following scopes in PagerDuty new app registration setting page.

   ·    Audit records – Read Access

   ·    Schedules – Read Access

   ·    Teams – Read Access

   ·    Users – Read Access

8. After you successfully complete app registration in PagerDuty, copy Client ID and Client Secret.

## Get started

### 1. Choose display name   
Choose a display name that helps users easily recognize associated files or items in a Copilot response.

### 2. Instance REST API URL
PagerDuty allows customers to choose the geographic service region of the PagerDuty data centers that host their account. 

- For US service region, REST API URL is https://api.pagerduty.com.
- For EU service region, REST API URL is https://api.eu.pagerduty.com.

See [Service Regions](https://support.pagerduty.com/main/docs/service-regions) for more information.

### 3. Choose authentication type
Enter the Client ID and Client Secret you obtained from your PagerDuty app registration setting.

### 4. Roll out to a limited audience
Deploy this connection to a limited user base to validate it in Copilot and other search surfaces before you roll it out to a broader audience.

## Custom setup 

Custom setup is for admins who want to edit the default values for the settings. When you choose **Custom setup**, you see three other tabs: **Users**, **Content**, and **Sync**. 

### Users 

**Access permissions**

Determine which users in your organization can access each item in Copilot or Search surfaces. Choose whether indexed data is visible to everyone in the organization or only to users who have access to the data source.

### Content 

**Content Filter**

Two extra parameters can be used to specify the date range for crawling final schedule content in PagerDuty.
•	Days Before
•	Days After

The crawl start date is (Today – Days Before) and the crawl end date is (Today + Days After).

**Manage properties**

You can add or remove available properties from your PagerDuty Schedule data source. Assign a schema, change the semantic label, and add an alias to the property. The following properties are indexed by default.

|Source property|Label|Description|
|--- | ---- | --- |
|Id |Not applicable  | Unique ID of the schedule. |
|HtmlUrl |`url`  | URL of the schedule in PagerDuty. |
|IconUrl |`IconUrl` |  |
|Coverage | Not applicable | The percentage of the time range covered by this schedule. |
|CreatedBy |`createdBy`  | The name of the user who created the schedule. |
|CreatedDateTime | `createdDateTime` | The time at which the schedule was created. |
|Description	| Not applicable | The description of the schedule. |
|FinalSchedule	| Not applicable | This is a list of entries in the final schedule, including user, the start time of the entry, the end time of the entry. |
|LastModifiedBy	| `lastModifiedBy` | The name of the user who last modified the schedule. |
|LastModifiedDateTime	| `lastModifiedDateTime` | The time at which the schedule was last modified. |
|Name	| `title` | The name of the schedule. |
|Summary	| Not applicable | A short-form, server-generated string by PagerDuty that provides succinct, important information about an object suitable for primary labeling of an entity in a client. In many cases, this will be identical to `name`, though it is not intended to be an identifier. |
|Timezone	| Not applicable | The time zone of the schedule. |
|Usage	| Not applicable | The escalation policies associated with the schedule. |


### Sync 

Only full crawl is supported by PagerDuty Schedules connector. The default schedule of the full crawl is set for every day. If needed, you can adjust these schedules to fit your data refresh needs. 



## Troubleshooting

The following are common errors that can occur and how to resolve them.

**Your security credentials have expired for this session. Please go back and sign in again with your Client ID and Client secret.**

Credential info has expired. Please create a new app id in PagerDuty app registration setting and copy the latest Client ID and Client secret from the setting tab to authenticate.

 **Invalid Credentials detected. Please check the credential info and check the permission scopes of the PagerDuty App.**

Common credential error. Please go back to the PagerDuty app registration setting and check if the Client ID and Client secret have the correct permission scope.

## Next steps

After you publish your connection, you can review the status under the **Data sources** tab in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, see [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
