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

The Veeva Vault PromoMats Microsoft Graph connector allows organizations to index index promotional marketing materials from Veeva Vault into Microsoft Graph, making them accessible across Microsoft 365 experiences, including Microsoft 365 Copilot.

The connector integrates Vault PromoMats' built-in permission model, ensuring that users only access authorized content, and supports faster content generation and review through content analysis and preparation. By enhancing efficiency throughout the content lifecycle, it helps maintain brand consistency. This functionality is beneficial for marketing, medical affairs, and regulatory teams, enabling informed decision-making and reducing the time-to-market for promotional materials.

The following are the key benefits of the Veeva Vault PromoMats Microsoft Graph connector:

- **Enhanced content management and retrieval:** The connector suggests tags to organize and access relevant documents more easily.
- **AI-assisted content reuse and localization:** Facilitates content adaptation for various markets, saving time while ensuring relevance for different audiences.
- **Comprehensive document review and summarization:** AI tools help grammar, spelling, semantics, and regulatory compliance, ensuring accuracy and up-to-date promotional materials.

Additionally, the connector boosts productivity by minimizing time spent searching for information across multiple sources. By integrating Microsoft 365 Copilot and Microsoft Search with PromoMats data, it streamlines content preparation and field use. It also improves efficiency by referencing existing compliant documents and content to help generate new messaging and prepare materials effectively.

This guide is for Microsoft 365 administrators or anyone responsible for configuring, managing, and monitoring the Veeva Vault PromoMats Microsoft Graph connector.

## Capabilities

- Generates summaries to understand and make decisions based on promotional materials and key documents.
- Improves the searchability of promotional documents by using advanced Microsoft 365 search capabilities.
- Gains insights and recommendations from indexed data to enhance workflow efficiency, including checking the usage of specific phrases in PromoMats documents.
- Indexes PromoMats content to create a unified search experience across Microsoft 365 environments.
- Maintains data privacy and compliance by supporting ACL permissions and document-level permissions, simplifying the permission model and reducing the risk of misconfiguration.
- Uses query string conditions to precisely control the synchronization of articles, ensuring efficient indexing.

### Examples

The following table lists example prompts that show how Microsoft 365 Copilot, integrated with the Veeva PromoMats Microsoft Graph connector, can significantly enhance productivity and streamline processes by using PromoMats data.

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
- Supports file types including Microsoft Office documents, PDFs, and text-based files only; does not support PNG, JPG, or video files.
- Partially indexes files larger than 4 MB.

## Prerequisites

- Make sure that you have a Veeva Vault account with administrative privileges.
- Enable the API access in your Veeva Vault instance.
- Activate REST API access in your Veeva Vault instance. For more information, see [Veeva Vault API documentation](https://developer.veevavault.com/docs/).
- Verify the URL for your Veeva Vault instance. The following is the typical URL format: `https://<your-vault-domain>.veevavault.com`


## Get started

### Step 1: Configure display name
Provide a meaningful display name for your connector in the Microsoft 365 Admin Center. This name helps identify the connection in your workspace.

### Step 2: Add the Veeva Vault URL
Enter the verified URL of your Veeva Vault instance. For example: `https://<your-vault-domain>.veevavault.com`.

### Step 3: Authentication details

To configure the Veeva Vault - PromoMats connector, you must provide authentication credentials. 
The connector supports the following authentication methods: 

#### Basic authentication 

- The username associated with your Veeva Vault account. 

- The password for the account. Keep this credential secure. 

#### Entra ID authentication 
This method applies Entra ID for secure and centralized identity management. The following are the required fields.

- **Vault session ID URL:** The URL endpoint for retrieving session tokens. Typically formatted as: `https://<your-vault-domain>.veevavault.com/api/v<version>/session`. 

- **Client ID:** The application ID for your Azure AD app registered for Veeva Vault. 

- **Client secret:** The client secret associated with the Entra ID  app. Make sure that it is securely stored and accessible only to authorized personnel. 
 
> [!Important]
> Configure both Microsoft Entra ID and Veeva Vault admin settings to enable Microsoft Entra ID authentication.

### Step 4: Rollout to limited audience
Deploy this connection to a limited group of users to validate indexing and access control functionality before a full rollout. 

### Step 5: Customize sync schedules
Set up periodic incremental crawls (default: 15 minutes) and full crawls (default: daily). 

## Default settings

| Section  | Setting               | Default value |
|----------|-----------------------|---------------|
| **Users**   | Access permissions   | Respects Veeva Vault permissions; only viewable documents are accessible. |
| **Content** | Index metadata       | Indexes key metadata, such as document name, owner, and lifecycle stage. |
| **Content** | Manage properties    | Enables metadata like title, created by, and last modified by. |
| **Sync**    | Full crawls          | Every day.|
| **Sync**  | Full crawl frequency|Every day.|

To modify these default values, click **Custom setup** during the configuration.

## Custom setup

### Users

**Access permissions**
The connector adheres to the ACLs defined in Veeva Vault. Only users with view permissions in Veeva Vault can see the indexed content in Microsoft 365. Admins can optionally allow all users access to all indexed content, although this isn't recommended.

### Sync

**Adjust sync schedules**  
You can modify the frequency of full crawls to fit your organization's requirements.
- Incremental Crawl: Default is 15 minutes. 
- Full Crawl: Default is daily.


## Troubleshooting

For information about troubleshooting, see [Troubleshooting guide](troubleshoot-veeva-vault-promomats-connector.md).

## Next steps

After the connector is configured and published, monitor its status on the **Data sources** in the [Admin Center](https://admin.microsoft.com). For more information, see [Manage your connector](manage-connector.md) guide.

For help and support, see [Microsoft Graph support](https://developer.microsoft.com/graph/support). 
