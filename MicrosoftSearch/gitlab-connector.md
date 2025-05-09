---
title: "GitLab Microsoft Graph connectors"
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
description: "Set up the GitLab Microsoft Graph connectors for Microsoft Search and Microsoft 365 Copilot."
ms.date: 02/14/2025
---

# GitLab Microsoft Graph connectors

The GitLab Microsoft Graph connectors (GitLab Issue, GitLab Merge Request, and GitLab Knowledge) allow your organization to index merge requests, issues, wikis, and documentation stored in GitLab. After you configure the connector and index GitLab content, users can search and retrieve information via Microsoft Search and Microsoft 365 Copilot.

This article is intended for Microsoft 365 administrators or anyone who configures, runs, or monitors GitLab Microsoft Graph connectors.

## Capabilities

- Index GitLab repositories, merge requests, and access issues, wikis, and documentation.
- Enable Microsoft Search and Microsoft 365 Copilot to retrieve GitLab data efficiently.
- Maintain GitLab ACLs and user permissions.
- Allow administrators to customize crawl frequency and indexing preferences.

## Limitations

- The connector does not support indexing GitLab CI/CD pipelines beyond status indexing.
- Only repositories, issues, merge requests, .md, .txt files, and wikis are indexed.
- Banning users is not supported as a permission rule. As a workaround, administrators can remove users from groups instead.
- Restricting group access by IP address is not supported. We recommend that administrators create a private group to manage access.
- Due to stability concerns identified during Microsoft's internal testing, support for the Planner role has been conservatively deprecated. Access is now restricted to Reporter roles and above. Users may encounter issues when assigning team members to the Planner role. To mitigate potential problems, please assign Reporter roles or higher. We closely monitor this feature and continue to work on improvements.
- For the GitLab Server connectors, due to security consideration, access to merge requests for public projects with visibility restricted to project members is conservatively set to the reporter role and above.

## Prerequisites

Before setting up the connector, ensure the following:

1. Confirm your GitLab instance is accessible via API.
2. Generate a **Client ID** and **Client Secret** from GitLab for authentication.
3. The authentication user account must have access to repositories, issues, merge requests, knowledge files, and wiki pages.  
   - Repositories  
   - Issues  
   - Merge requests  
   - Knowledge files  
   - Wiki pages  
4. The **Client ID** and **Client Secret** must include the following scopes:
   - `read_api`  
   - `read_repository`  
5. Users who will access the indexed GitLab data must have corresponding **Microsoft Entra ID** identities for permission mapping.
6. Set the appropriate **redirect URLs** during GitLab authentication setup:
   - **Microsoft 365 Enterprise**:  
     `https://gcs.office.com/v1.0/admin/oauth/callback`
   - **Microsoft 365 Government**:  
     `https://gcsgcc.office.com/v1.0/admin/oauth/callback`
  
### GitLab Server Connector Specifics

For **self-managed GitLab instances**, ensure the following:

1. **GitLab Version**: Must be 17.7 or later.
2. **Microsoft Graph Connector Agent**:
   - Version must be **3.1.8.0 or later**.
   - Must be installed on a server that can connect to the GitLab instance.  
   - Follow the [setup guide](./graph-connector-agent.md) to configure the agent.
3. The authentication account must have **administrative privileges** to enable ACL crawling.
4. **API Rate Limits**:  
   For best performance, disable or raise limits in the **User and IP rate limits** settings. Refer to the [GitLab documentation](https://docs.gitlab.co.jp/ee/user/admin_area/settings/user_and_ip_rate_limits.html#:~:text=On%20the%20left%20sidebar%2C%20select%20Settings%20%3E%20Network%2C,period%20per%20IP%20value.%20Defaults%20to%203600.%20Optional.).

   Recommended configuration:

   - **User and IP Rate Limits**:
     - Uncheck: `Enable authenticated API request rate limit`  
     - Uncheck: `Enable authenticated web request rate limit`

   - **Files API Rate Limits**:
     - Uncheck: `Enable authenticated API request rate limit`

   - **Deprecated API Rate Limits**:
     - Uncheck: `Enable authenticated API request rate limit`

   - **Users API Rate Limits**:
     - Set `Max requests per 10 minutes per user` to a high value (e.g., `100000`)

   - **Groups API Rate Limits**:
     - Set all values to `0` to disable limits

   - **Projects API Rate Limits**:
     - Set all values to `0` to disable limits

   - **Members API Rate Limits**:
     - Set to `0`

## Get started

### 1. Choose display name
Choose a display name that helps users recognize merge requests, issues, or documentation in a Copilot response.

### 2. Authenticate

- Enter your **Client ID** and **Client secret** from GitLab.
- Choose **Authorize** to sign in and grant access.
- Grant the required API scopes.

### 3. Roll out to limited audience
Before you deploy the connector, test the connection with a limited user base in Copilot and Microsoft Search.

## Custom setup
Custom setup is for admins who want to edit the default values for any settings. When you choose **Custom setup**, you see three other tabs: **Users**, **Content**, and **Sync**. 

### Users
#### Identity mapping
To ensure correct permission enforcement, map GitLab user identities to Microsoft Entra ID. The following are the options:
  - **Email:** Matches GitLab user emails with Microsoft Entra ID emails. (Default and recommended mapping)
  - **Username:** Matches GitLab user names to Microsoft Entra ID user principal name (UPN).
  - **Name:** Maps GitLab user names with Microsoft Entra ID display names.

If direct mapping fails, use **regular expressions (regex)** for transformation.

### Content
You can verify property mappings in the sample data for metadata such as **titles**, **descriptions**, **statuses**, and **timestamps** on the **Content** tab.

### Sync
You can configure **incremental** and **full** crawls. The following are the default values:

  - Incremental crawl runs **every 15 minutes** by default.
  - Full crawl runs **daily** to ensure up-to-date indexing.

## Next steps

- Review the connection status in the Microsoft 365 admin center. 
- For troubleshooting information, see the [GitLab troubleshooting guide](troubleshoot-gitlab-connector.md).
- If you have issues or need support, see [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
