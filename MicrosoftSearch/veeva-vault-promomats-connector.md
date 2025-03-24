--- 

title: "Veeva Vault PromoMats Microsoft Graph connector" 
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
description: "Set up the Veeva Vault PromoMats Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot" 
ms.date: 02/26/2025
---
# Veeva Vault PromoMats Microsoft Graph connector

The Veeva Vault PromoMats Microsoft Graph connector allows organizations to index promotional marketing materials from Veeva Vault into Microsoft Graph, making them accessible across Microsoft 365 experiences, including Microsoft 365 Copilot.

The connector integrates Vault PromoMats' built-in permission model, ensuring that users only access authorized content, and supports faster content generation and review through content analysis and preparation. By enhancing efficiency throughout the content lifecycle, it helps maintain brand consistency. This functionality is beneficial for marketing, medical affairs, and regulatory teams, enabling informed decision-making and reducing the time-to-market for promotional materials.

The following are the key benefits of the Veeva Vault PromoMats Microsoft Graph connector:

- **Enhanced content management and retrieval:** The connector suggests tags to organize and access relevant documents more easily.
- **AI-assisted content reuse and localization:** Facilitates content adaptation for various markets, saving time while ensuring relevance for different audiences.
- **Comprehensive document review and summarization:** AI tools help grammar, spelling, semantics, and regulatory compliance, ensuring accuracy and up-to-date promotional materials.

Additionally, the connector boosts productivity by minimizing time spent searching for information across multiple sources. By integrating Microsoft 365 Copilot and Microsoft Search with PromoMats data, it streamlines content preparation and field use. It also improves efficiency by referencing existing compliant documents and content to help generate new messaging and prepare materials effectively.

This guide is for Microsoft 365 administrators or anyone responsible for configuring, managing, and monitoring the Veeva Vault PromoMats Microsoft Graph connector.

## Capabilities

The Veeva Vault PromoMats connector enables the following capabilities:

- Generates summaries to understand and make decisions based on promotional materials and key documents.
- Improves the searchability of promotional documents by using advanced Microsoft 365 search capabilities.
- Gains insights and recommendations from indexed data to enhance workflow efficiency, including checking the usage of specific phrases in PromoMats documents.
- Indexes PromoMats content to create a unified search experience across Microsoft 365 environments.
- Maintains data privacy and compliance by supporting ACL permissions and document-level permissions, simplifying the permission model and reducing the risk of misconfiguration.
- Uses query string conditions to precisely control the synchronization of articles, ensuring efficient indexing.

The following table lists example prompts that show how Microsoft 365 Copilot, integrated with the Veeva PromoMats connector, can significantly enhance productivity and streamline processes by using PromoMats data.

|Scenario|Example prompt|
|:---|:---|
|Content generation|Generate personalized content for customer interactions based on the latest research documents stored in PromoMats.|
|Content tagging|Suggest tags that can be used with the selected promotional contents to make it easier to manage and retrieve going forward.|
| HTML email generation|Create HTML emails generated automatically from pre-provided HTML templates and documents stored in PromoMats.|
|Pre-call planning|Summarize relevant information and prepare materials for sales representatives before customer meetings.|
|AI-assisted content re-use|Identify appropriate tags, translation, and localization to improve the reuse of content. |
|Content consistency|Create new promotional materials, ensuring consistency with existing content.|
|Pre-MLR AI-assisted reviews|Review grammar, spelling, and semantics and cross-validate the following promotional documents.|
|Document summarization|Summarize key points from regulatory documents to ensure all team members are informed of the latest compliance requirements.|
|Meeting preparation|Prepare a script for an upcoming meeting based on recent customer email threads and PromoMats documents.|
|Support claim process|Find claims that can be reused made about the efficacy of drugs to ensure they are medically and legally validated and approved.|

## Limitations

- Indexes only the latest versions of documents.
- Supports file types including Microsoft Office documents, PDFs, and text-based files only; doesn't support PNG, JPG, or video files.
- Partially indexes files larger than 4 MB.

## Prerequisites
### Configure Microsoft Entra ID OAuth 2.0/OpenID Connect for Veeva Vault Microsoft Graph connector

#### Step 1: Register an application in Microsoft Entra ID

1. Go to **Microsoft Entra admin center** > **Applications** > **Register a new application**.

2. Set up API permissions:
   - Add **Microsoft Graph** > **Delegated permissions**.
   - Include scope: `offline_access {clientId}/.default`
   - Grant **Admin Consent**.

3. Under **Certificates & Secrets**, generate a client secret and store it securely.

4. In the **OAuth 2** section of the **Setting** tab in the Veeva Vault app console, add the following links to the **Redirect URLs** field:
   - For **Microsoft 365 Enterprise**, copy and paste:
     `https://gcs.office.com/v1.0/admin/oauth/callback`
   - For **Microsoft 365 Government**, copy and paste:
     `https://gcsgcc.office.com/v1.0/admin/oauth/callback`

#### Step 2: Configure OAuth in Veeva Vault

1. Go to **Admin** > **Settings** > **OAuth 2.0 / OpenID Connect Profiles**.

2. Create a new profile:
   - **Authorization Server Provider:** Azure
   - **Upload Microsoft Entra ID Metadata:** Use the following URL:
     `https://login.microsoftonline.com/{tenantId}/v2.0/.well-known/openid-configuration`
   - **Identity Claim:** Use the appropriate **Identity Claim** to associate the identities of Microsoft Entra ID and Veeva Vault.

3. Add the client application. Use the **Client ID** from Entra ID.

4. Activate the profile and link it to a security policy under **Users & Groups > Security Policies**.

## Get started


### 1. Configure display name
Provide a meaningful display name for your connector in the Microsoft 365 Admin Center. This name helps identify the connection in your workspace.

### 2. Add the Veeva Vault URL
Enter the verified URL of your Veeva Vault instance. For example: `https://<your-vault-domain>.veevavault.com`.

### 3. Provide authentication details

To configure the Veeva Vault PromoMats connector, you must provide authentication credentials. 
The connector supports basic authentication and Entra ID authentication.

#### Basic authentication 

#### Microsoft Entra ID Authentication
To use Microsoft Entra ID authentication, you need the following:
- **Vault Session ID URL**:  
  Format: `https://login.veevavault.com/auth/oauth/session/{oath_oidc_profile_id}`
- **Client ID**: The application ID of your Microsoft Entra ID app registered for Veeva Vault.
- **Client secret**: The corresponding client secret. Securely store and restrict access to this value.

#### Entra ID authentication 

method applies Entra ID for secure and centralized identity management. The following are the required fields:

- **Vault session ID URL:** The URL endpoint for retrieving session tokens. Typically formatted as: `https://<your-vault-domain>.veevavault.com/api/v<version>/session`. 
- **Client ID:** The application ID for your Azure AD app registered for Veeva Vault. 
- **Client secret:** The client secret associated with the Entra ID  app. Make sure that it is securely stored and accessible only to authorized personnel. 
 
> [!Important]
> Configure both Microsoft Entra ID and Veeva Vault admin settings to enable Microsoft Entra ID authentication.

### 4. Rollout to limited audience
Deploy this connection to a limited group of users to validate indexing and access control functionality before a full rollout. 

### 5. Customize sync schedules
Set up periodic incremental crawls (default: 15 minutes) and full crawls (default: daily). 

## Default settings

The following table lists the default settings for the Veeva Vault PromoMats Microsoft Graph connector. To modify these default values, choose **Custom setup** during the configuration.

| Section  | Setting               | Default value |
|----------|-----------------------|---------------|
| **Users**   | Access permissions   | Respects Veeva Vault permissions; only viewable documents are accessible. |
| **Content** | Index metadata       | Indexes key metadata, such as document name, owner, and lifecycle stage. |
| **Content** | Manage properties    | Enables metadata like title, created by, and last modified by. |
| **Sync**    | Full crawls          | Every day.|
| **Sync**  | Full crawl frequency|Every day.|

## Custom setup

### Users

#### Access permissions

The connector adheres to the ACLs defined in Veeva Vault. Only users with view permissions in Veeva Vault can see the indexed content in Microsoft 365. Admins can optionally allow all users access to all indexed content, although this isn't recommended.

### Sync

#### Adjust sync schedules

You can modify the frequency of full crawls to fit your organization's requirements. The following are the default crawls:

- Incremental crawl - 15 minutes.
- Full crawl - daily.


## Troubleshooting

For information about troubleshooting, see [Troubleshooting the Veeva Vault Microsoft Graph connector](troubleshoot-veeva-vault-connectors.md).

## Next steps

After you configure and publish the connector, monitor its status on the **Data sources** tab in the [Admin Center](https://admin.microsoft.com). For more information, see [Manage your connector](manage-connector.md).

For help and support, see [Microsoft Graph support](https://developer.microsoft.com/graph/support). 
