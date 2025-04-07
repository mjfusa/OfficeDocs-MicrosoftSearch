---
title: "Veeva Vault QualityDocs Microsoft Graph connector (preview)" 
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
description: "Set up the Veeva Vault QualityDocs Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot." 
ms.date: 02/26/2025
---

# Veeva Vault QualityDocs Microsoft Graph connector (preview)

The Veeva Vault QualityDocs Microsoft Graph connector allows organizations to index quality and compliance documents from Veeva Vault into Microsoft Graph, making them accessible across Microsoft 365 experiences, including Microsoft 365 Copilot.

The connector integrates the Vault QualityDocs built-in permission model, ensuring that users only access authorized content, and supports faster content retrieval and review through content analysis and preparation. By enhancing efficiency throughout the document lifecycle, it helps maintain compliance and quality control. This functionality enables informed decision-making and reduces time-to-approval for critical documents to benefit quality management, regulatory, and manufacturing teams.

The following are the key benefits of the Veeva Vault QualityDocs Microsoft Graph connector:

- **Enhanced document management and retrieval:** The connector suggests tags to organize and access relevant documents more easily.
- **AI-assisted document reuse and compliance checks:** Facilitates document validation for various regulatory needs, saving time while ensuring adherence to quality standards.
- **Comprehensive document review and summarization:** AI tools help grammar, spelling, semantics, and compliance verification, ensuring accuracy and up-to-date quality documents.

Additionally, the connector boosts productivity by minimizing time spent searching for information across multiple sources. By integrating Microsoft 365 Copilot and Microsoft Search with QualityDocs data, it streamlines compliance processes and audit readiness. It also improves efficiency by referencing existing approved documents to support document updates and quality workflows.

This guide is for Microsoft 365 administrators or anyone responsible for configuring, managing, and monitoring the Veeva Vault QualityDocs Microsoft Graph connector.

## Capabilities

The Veeva Vault QualityDocs connector enables the following capabilities:

- Generates summaries to understand and make decisions based on quality and compliance documents.
- Improves the searchability of quality documents by using advanced Microsoft 365 search capabilities.
- Gains insights and recommendations from indexed data to enhance workflow efficiency, including checking document approvals and compliance status.
- Indexes QualityDocs content to create a unified search experience across Microsoft 365 environments.
- Maintains data privacy and compliance by supporting ACL permissions and document-level permissions, simplifying the permission model and reducing the risk of misconfiguration.
- Uses query string conditions to precisely control the synchronization of documents, ensuring efficient indexing.

The following table lists example prompts that show how Microsoft 365 Copilot, integrated with the Veeva QualityDocs connector, can significantly enhance productivity and streamline processes by using QualityDocs data.

|Scenario|Example prompt|
|:---|:---|
|Document review|Summarize key points from quality and compliance documents to ensure all team members are informed of the latest regulatory requirements.|
|Audit preparation|Generate a compliance checklist based on stored quality documents.|
|Document tagging|Suggest tags that can be used with the selected quality documents to improve retrieval.|
|Compliance validation|Identify documents that require compliance updates and generate a report.|
|Quality consistency|Ensure new quality documents align with existing approved documentation.|
|Meeting preparation|Prepare an agenda for an upcoming regulatory review meeting based on recent compliance reports.|

## Limitations

- Indexes only the latest versions of documents.
- Supports file types including Microsoft Office documents, PDFs, and text-based files only; does not support PNG, JPG, or video files.
- Partially indexes files larger than 4 MB.

## Prerequisites: 
### Configuring Microsoft Entra ID OAuth 2.0/OpenID Connect for Veeva Vault Microsoft Graph Connector

#### Step 1: Register an application in Microsoft Entra ID

1. Go to **Microsoft Entra admin center** > **Applications** > **Register a new application**.
2. **Set up API permissions:**
   - Add **Microsoft Graph** > **Delegated permissions**
   - Include scope: `offline_access {clientId}/.default`
   - Grant **Admin Consent**.
3. Under **Certificates & Secrets**, generate a client secret and store it securely.
4. In the **OAuth 2** section of the **Setting** tab in the Veeva Vault app console, add the following links to the **Redirect URLs** field:
   - For **Microsoft 365 Enterprise**, copy and paste: `https://gcs.office.com/v1.0/admin/oauth/callback`.
   - For **Microsoft 365 Government**, copy and paste: `https://gcsgcc.office.com/v1.0/admin/oauth/callback`.

#### Step 2: Configure OAuth in Veeva Vault

1. Go to **Admin** > **Settings** > **OAuth 2.0 / OpenID Connect Profiles**.
2. Create a new profile:
   - **Authorization Server Provider:** Azure
   - **Upload Microsoft Entra ID Metadata:** Use the following URL: `https://login.microsoftonline.com/{tenantId}/v2.0/.well-known/openid-configuration`.
   - **Identity Claim:** Use the appropriate **Identity Claim** to associate the identities of Microsoft Entra ID and Veeva Vault.
3. **Add client application:** Use the **Client ID** from Entra ID.
4. **Activate the profile** and link it to a security policy under **Users & Groups > Security Policies**.

## Get started

### 1. Configure display name
Provide a meaningful display name for your connector in the Microsoft 365 Admin Center. This name helps identify the connection in your workspace.

### 2. Add the Veeva Vault URL
Enter the verified URL of your Veeva Vault instance. For example: `https://<your-vault-domain>.veevavault.com`.

### 3. Provide authentication details

The connector supports basic authentication and Entra ID authentication.

### 4. Roll out to limited audience
Deploy this connection to a limited group of users to validate indexing and access control functionality before a full rollout. 

### 5. Customize sync schedules
Set up periodic incremental crawls (default is 15 minutes) and full crawls (default is daily). 

## Default settings

The default settings for the Veeva Vault QualityDocs connector are the same as those for the [Veeva Vault PromoMats connector](veeva-vault-promomats-connector.md#default-settings).

## Troubleshooting

For troubleshooting information, see [Troubleshooting the Veeva Vault Microsoft Graph connectors](troubleshoot-veeva-vault-connectors.md).

## Next steps

After you configure and publish the connector, monitor the status in the **Data sources** tab in the [Admin Center](https://admin.microsoft.com). For more information, see [Manage your connector](manage-connector.md) guide.

For help and support, see [Microsoft Graph support](https://developer.microsoft.com/graph/support).
