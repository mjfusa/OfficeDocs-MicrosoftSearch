---
title: "GitLab Microsoft Graph Connector for Microsoft Search and Copilot"
ms.author: dannyyao
author: dannyyaou
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
description: "Set up the v Graph Connector for Microsoft Search and Copilot"
ms.date: 02/14/2025
---

# GitLab Microsoft Graph Connectors

The GitLab Microsoft Graph Connectors (GitLab Issue, GitLab Merge Request, and GitLab Knowledge) allows your organization to index merge requests, issues, wikis, and documentation stored in GitLab. After configuring the connector and indexing GitLab content, end users can search and retrieve information via Microsoft Search and Microsoft 365 Copilot.

This article is intended for Microsoft 365 administrators or anyone configuring, running, and monitoring GitLab Microsoft Graph Connectors.

## Capabilities

- Index GitLab repositories, merge requests, issues, wikis, and documentation.
- Enable Microsoft Search and Microsoft 365 Copilot to retrieve GitLab data efficiently.
- Maintain GitLab access control lists (ACLs) and user permissions.
- Allow administrators to customize crawl frequency and indexing preferences.

## Limitations

- The connector does not support indexing GitLab CI/CD pipelines beyond status indexing.
- Only repositories, issues, merge requests, .md, .txt files and wikis are indexed.
- On-premises/self-hosted GitLab instances are supported in a later release.

## Prerequisites

Before setting up the connector, ensure that:

1. Your GitLab instance is accessible via API.
2. You have generated a **Client ID** and **Client Secret** from GitLab for authentication.
3. The user account used for authentication has access to the repositories, issues, merge requests, knowledge files, and wiki pages to be indexed.
4. The **Client ID** and **Client Secret** have the `read_api` permission scope.
5. Users accessing indexed GitLab data have corresponding **Microsoft Entra ID (Azure AD)** identities for permission mapping.

## 1-Click Setup Process

### 1. Display Name
Choose a display name that helps users easily recognize associated merge requests, issues, or documentation in a Copilot response.

### 2. Authentication
- Enter your **Client ID** and **Client Secret** from GitLab.
- Click **Authorize** to log in and grant access.
- Ensure that the required API scopes are granted.

### 3. Rollout to Limited Audience
Before a full deployment, you can test the connection with a **limited user base** in Copilot and Microsoft Search.

## Custom Setup
Custom setup is for those admins who want to edit the default values for settings listed in the above table. Once you click on the "Custom Setup" option, you see three more tabs - Users, Content, and Sync.

### Users
#### Identity Mapping
To ensure correct permission enforcement:
- Map GitLab user identities to Microsoft Entra ID (Azure AD).
- Options include:
  - **Email (Recommended, Default):** Matches GitLab user emails with Microsoft Entra ID emails.
  - **Username:** Matches GitLab usernames to Microsoft Entra ID userPrincipalName (UPN).
  - **Name:** Maps GitLab user names with Microsoft Entra ID display names.
- If direct mapping fails, use **regular expressions (regex)** for transformation.

### Content
You can verify property mappings in the sample data for metadata such as **titles, descriptions, statuses, and timestamps** in the Content tab.

### Sync
- You can configure **incremental** and **full** crawls, by default:
  - Incremental crawl runs **every 15 minutes** by default.
  - Full crawl runs **daily** to ensure up-to-date indexing.



## Next Steps
After setup, review the connection status in the **Microsoft 365 Admin Center**.  
For troubleshooting, refer to the [GitLab Graph Connector Troubleshooting Guide](troubleshooting-gitlab-graph-connector.md).

If you experience issues or need support, visit [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
