--- 

title: "Guru Microsoft Graph connector" 
ms.author: rantang
author: ranran1998
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
description: "Set up the Guru Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot" 
ms.date: 3/14/2025
---

# Guru Microsoft Graph connector (preview)

With the Guru Microsoft Graph connector, your organization can index Tableau cards of your Guru. After you configure the connector and index content from Guru, end users can search for those  cards in Microsoft Copilot and from any Microsoft Search client. h.

This article is for Microsoft 365 administrators or anyone who configures, runs, and monitors an Guru Microsoft Graph connector. 

## Capabilities
- Index cards of your Guru and supports ingestion filters based on top-level projects.
- Retain access control lists (ACLs) defined by your organization
- Customize your crawl frequency.
- Create workflows using this connection and plugins from Microsoft Copilot Studio.  
- Use [Semantic search in Copilot](semantic-index-for-copilot.md) to enable users to find relevant content.

## Limitations
- cards in personal space aren't indexable

## Prerequisites
- You must be the **search admin** for your organization's Microsoft 365 tenant.
- **Configure Connected Apps with Direct Trust in Tableau**: To connect to Guru and allow the Guru Microsoft Graph connector to update cards regularly, you need to configure and enable the Connected Apps with Direct Trust of your Tableau Site with the credentials to access cards. Tableau connected apps enable a seamless and secure authentication experience by facilitating an explicit trust relationship between your Guru site and external applications. Find more details [here](https://help.tableau.com/current/online/en-us/connected_apps_direct.htm?_gl=1*9bs6y1*_ga*MTk1OTAyNzg0MS4xNzIxMTIwMzA4*_ga_8YLN0SNXVS*MTczNTE5MzU5OS4zNC4xLjE3MzUyMDA1ODEuMC4wLjA.).

## Get started

### 1. Display name 
A display name is used to identify each citation in Copilot, helping users easily recognize the associated file or item. Display name also signifies trusted content. The display name is also used as a [content source filter](/MicrosoftSearch/custom-filters#content-source-filters). A default value is present for this field, but you can customize it to a name that users in your organization recognize.

### 2. Guru Site URL
A Guru site URL typically looks like https://<>.online.tableau.com/#/site/<> 

### 3. Authentication Type
We support the Connected Apps with OAuth2.0 Client Secret for Guru. To enable and configure the Connected Apps with Direct Trust for Guru, please find more details [here](https://help.tableau.com/current/online/en-us/connected_apps_direct.htm?_gl=1*9bs6y1*_ga*MTk1OTAyNzg0MS4xNzIxMTIwMzA4*_ga_8YLN0SNXVS*MTczNTE5MzU5OS4zNC4xLjE3MzUyMDA1ODEuMC4wLjA.).

### 4. Staged rollout to a limited audience
Deploy this connection to a limited user base if you want to validate it in Copilot and other Search surfaces before expanding the rollout to a broader audience.

At this point, you are ready to create the connection for Guru. You can click the **Create** button to publish your connection and index cards from your Guru Site. 

For other settings, like Access Permissions, Data inclusion rules, Schema, Crawl frequency, etc., we set defaults based on what works best with Guru data. You can see the default values below: 

**Page** | **Settings** | **Default values**
--- | ---- | ---
Users | Access permissions | Only people with access to this data source.
Users | Map Identities |Data source identities mapped using Microsoft Entra IDs.
Content | Index content | All cards, except the cards in personal space. 
Content | Manage properties | To check default properties and their schema, [click here](#content).
Sync | Incremental crawl | Frequency: Every 15 mins
Sync | Full crawl | Frequency: Every day

If you want to edit any of these values, you need to choose the **Custom setup** option. 

## Custom setup 

Custom setup is for those admins who want to edit the default values for settings. Once you click the **Custom setup** option, you should see three other tabs – **Users**, **Content**, and **Sync**. 

### Users 

**Access permissions**

The Guru Microsoft Graph connector supports data visible to Only people with access to this data source (recommended) or Everyone. If you choose Everyone, indexed data appears in the search results for all users. 

If you choose Only people with access to this data source, you need to further choose whether your Guru Site has Microsoft Entra ID provisioned users or non-AAD users. 

To identify which option is suitable for your organization: 

1. Choose the **Microsoft Entra ID** option if the email ID of Guru users is same as the UserPrincipalName (UPN) of users in Microsoft Entra ID. 

2. Choose the **non-AAD** option if the email ID of Guru users is **different** from the UserPrincipalName (UPN) of users in Microsoft Entra ID.

>[!Important]
>- If you choose Microsoft Entra ID as the type of identity source, the connector maps the email IDs of users obtained from Guru directly to UPN property from Microsoft Entra ID.
>- If you chose "non-AAD" for the identity type see Map your non-Azure AD Identities for instructions on mapping the identities. You can use this option to provide the mapping regular expression from email ID to UPN.
>- Updates to users or groups governing access permissions are synced in full crawls only. Incremental crawls do not currently support the processing of updates to permissions.

### Content 

**Content ingestion filters**   

You can choose what data you want to index. All cards within the selected top-level project of your Guru Site will be indexed. Use the preview results button to verify the sample values of the selected properties and filters. 

Use the preview results button to verify the sample values of the selected properties and filters. 

**Manage properties**

Here, you can check available properties from your Guru. Assign a schema to the property (define whether a property is searchable, queryable, retrievable, or refinable), change the semantic label, and add an alias to the property. Properties that are selected by default are listed below. | Properties       | Semantic Label           | Schema                         |

| **CreatedAt**       | **Created date time**       | **Query, Retrieve**              |
|-----------------|-------------------------|--------------------------------|
| IconUrl         | IconUrl                  | Retrieve                       |
| LastModifiedBy  | Last modified by        | Query, Retrieve, Search        |
| Name           | Title                    | Query, Retrieve, Search        |
| ProjectName     |                          | Query, Search                  |
| SheetType       |                          | Query, Refine, Retrieve        |
| SheetUrl        | url                      | Retrieve                       |
| Tags           |                          | Query, Refine, Retrieve        |
| TopProjectName  |                          | Query, Search                  |
| UpdatedAt       | Last modified date time | Query, Retrieve               |
| WorkbookName    |                          | Query, Search                  |
| WorkbookUrl     |                          |                                |

### Sync 

You can configure full and incremental crawls based on the scheduling options present here. By default, incremental crawl is set for every 15 minutes, and full crawl is set for every day. If needed, you can adjust these schedules to fit your data refresh needs.

## Troubleshooting
After publishing your connection, you can review the status under the **Data sources** tab in the [admin center](https://admin.microsoft.com). To learn how to make updates and deletions, see [Manage your connector](manage-connector.md).

If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
