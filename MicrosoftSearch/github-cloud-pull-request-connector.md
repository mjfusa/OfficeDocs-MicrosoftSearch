---
title: "GitHub Cloud Pull Request Microsoft Graph connector (preview)"
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
description: "Set up the GitHub Cloud Pull Request Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot."
ms.date: 02/14/2025
---

# GitHub Cloud Pull Request Microsoft Graph connectors (preview)

The GitHub Cloud Pull Request Microsoft Graph connectors allow your organization to index pull requests stored in GitHub. After you configure the connector and index GitHub content, users can search and retrieve information via Microsoft Search and Microsoft 365 Copilot.

This article is intended for Microsoft 365 administrators or anyone who configures, runs, or monitors GitHub Cloud Pull Request Microsoft Graph connectors.

## Capabilities

- Index GitHub pull requests.
- Enable Microsoft Search and Microsoft 365 Copilot to retrieve GitHub data efficiently.
- Maintain GitHub ACLs and user permissions.
- Allow administrators to customize crawl frequency and indexing preferences.

## Limitations

- The connector does not support indexing GitHub CI/CD pipelines beyond status indexing.
- On-premises/self-hosted GitHub instances aren't currently supported.
- Restricting group access by IP address is not supported. We recommend that administrators create a private group to manage access.
- Comments and the information about the commits are not crawled.

## Prerequisites

Before you set up the connector:

1. Make sure that your GitHub instance is accessible via API.
2. Set up a GitHub App for authentication. For more information, see [Authenticating as a GitHub App](https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app/authenticating-as-a-github-app).
3. Generate a **Client ID** and **Client secret** from the GitHub App for authentication.
4. Verify that the user account used for authentication has access to the repositories and pull requests to be indexed.
5. Verify that the client ID and client secret have permission to read the pull requests.
6. Make sure that users who access indexed GitHub data have corresponding **Microsoft Entra ID** identities for permission mapping.\*

\* We recommend that you use a different GitHub App for OAuth authentication for each connection, as GitHub's rate limit is calculated per GitHub App.

## Get started

### 1. Choose display name
Choose a display name that helps users recognize the connection in a Copilot response.

### 2. Authenticate

- Enter your **Client ID** and **Client secret** from your GitHub App.
- Choose **Authorize** to sign in and grant access.
- Grant the required API scopes.

### 3. Roll out to limited audience
Before you deploy the connector, test the connection with a limited user base in Copilot and Microsoft Search.

## Custom setup
Custom setup is for admins who want to edit the default values for any settings. When you choose **Custom setup**, you see three other tabs: **Users**, **Content**, and **Sync**. 

### Users
#### Identity mapping
To ensure correct permission enforcement, map GitHub user identities to Microsoft Entra ID. The following are the options:
  - **Email:** Matches GitHub email to Microsoft Entra ID user properties.
  - **Login:** Maps GitHub logins with Microsoft Entra ID user properties.
  - **Name:** Maps GitHub name with Microsoft Entra ID user properties.

If direct mapping fails, use **regular expressions (regex)** for transformation.

### Content
On the **Content** tab, you can verify property mappings in the sample data for metadata such as **content**, **labels**, **description**, and **timestamps**.

### Sync
You can configure incremental and full crawls. The following are the default values:

  - Incremental crawl runs every 15 minutes by default.
  - Full crawl runs daily to ensure up-to-date indexing.

## Next steps

- Review the connection status in the Microsoft 365 Admin Center. 
- If you have issues or need support, see [Microsoft Graph support](https://developer.microsoft.com/en-us/graph/support).
