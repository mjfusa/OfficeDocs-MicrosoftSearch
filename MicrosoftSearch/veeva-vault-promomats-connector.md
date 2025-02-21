--- 

title: "Veeva VaultPromoMats Microsoft Graph connector" 
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
ms.date: 12/02/2024
---
# Veeva Vault PromoMats Microsoft Graph connector (preview)

The  Veeva Vault PromoMats Microsoft Graph connector allows organizations to index index promotional marketing materials from Veeva Vault into Microsoft Graph, making them accessible across Microsoft 365 experiences, including Microsoft 365 Copilot.

The connector integrates Vault PromoMats' built-in permission model, ensuring that users only access authorized content, and supports faster content generation and review through content analysis and preparation. By enhancing efficiency throughout the content lifecycle, it helps maintain brand consistency. This functionality is particularly beneficial for marketing, medical affairs, and regulatory teams, enabling informed decision-making and reducing the time-to-market for promotional materials.

Key benefits include enhanced content management and retrieval, as the connector suggests tags to make it easier to organize and access relevant documents. It also supports AI-assisted content reuse and localization, which facilitates content adaptation for various markets, saving time while ensuring content remains relevant and well-suited for different audiences. The connector offers comprehensive document review and summarization, with AI tools assisting in grammar, spelling, semantics, and regulatory compliance, ensuring promotional materials are accurate and up-to-date.

Additionally, the connector boosts productivity by minimizing the time spent searching for information across multiple sources. By integrating Microsoft 365 Copilot and Microsoft Search with PromoMats data, it streamlines content preparation and field use. It also improves efficiency by referencing existing compliant documents and content, helping to generate new messaging and prepare materials effectively.

This guide is for Microsoft 365 administrators or anyone responsible for configuring, managing, and monitoring the Veeva Vault PromoMats Microsoft Graph connector.

## Capabilities

- Generates summaries to understand and make decisions based on promotional materials and key documents.
- Improves the searchability of promotional documents by leveraging advanced Microsoft 365 search capabilities.
- Gains insights and recommendations from indexed data to enhance workflow efficiency, including checking the usage of specific phrases in PromoMats documents.
- Indexes PromoMats content to create a unified search experience across Microsoft 365 environments.
- Maintains data privacy and compliance by supporting ACL permissions and document-level permissions, simplifying the permission model and reducing the risk of misconfiguration.
- Uses query string conditions to precisely control the synchronization of articles, ensuring efficient indexing.

## Limitations

- Indexes only the latest versions of documents.
- Supports file types including Microsoft Office documents, PDFs, and text-based files.
- Indexes files up to 100 MB in size, extracting a maximum of 4 MB of text content per file.

## Prerequisites

- Ensure you have a Veeva Vault account with administrative privileges.
- Enable the API access in your Veeva Vault instance.
- Activate REST API access in your Veeva Vault instance. For more information, see [Veeva Vault API documentation](https://developer.veevavault.com/docs/).
- Verify the URL for your Veeva Vault instance. The format typically looks like:  
  `https://<your-vault-domain>.veevavault.com`


## Get started

To access the connector during the public preview phase, customer who are Microsoft 365 Admins need to enable 'Targeted release' for their tenant. For more information, see [Targeted release](https://learn.microsoft.com/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide#targeted-release).


### Step 1: Configure Display Name
Provide a meaningful display name in the Microsoft 365 Admin Center to identify the connector.

### Step 2: Add the Veeva Vault URL
Enter the verified URL of your Veeva Vault instance, for example
`https://<your-vault-domain>.veevavault.com`

### Step 3: Authentication details

To configure the Veeva Vault - PromoMats connector, you must provide authentication credentials. 
The connector supports the following authentication methods: 

#### Basic authentication 

- The username associated with your Veeva Vault account. 

- The password for the account. Ensure this credential is kept secure, as it's be used for authentication. 

#### Azure AD authentication 
This method leverages Azure Active Directory (AAD) for secure and centralized identity management. 
These are the required fields.

- Vault session ID URL: The URL endpoint for retrieving session tokens. Typically formatted as: `https://<your-vault-domain>.veevavault.com/api/v<version>/session`. 

- Client ID: The application ID for your Azure AD app registered for Veeva Vault. 

- Client secret: The client secret associated with the Azure AD app. Ensure this is securely stored and accessible only to authorized personnel. 
 
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
The connector adheres to the ACLs defined in Veeva Vault. Only users with view permissions in Veeva Vault can see the indexed content in Microsoft 365. Admins can optionally allow all users access to all indexed content, though this is not recommended.

### Sync

**Adjust sync schedules**  
You can modify the frequency of full crawls to fit your organization's requirements.
- Incremental Crawl: Default is 15 minutes. 
- Full Crawl: Default is daily.

## Examples


## Troubleshooting

For more information, see [Troubleshooting Guide](troubleshoot-veeva-vault-promomats-connector.md).

## Next steps

Once the connector is configured and published, monitor its status  **Data sources** in the [Admin Center](https://admin.microsoft.com). For more information, see [Manage your connector](manage-connector.md) guide.

If you have issues or want to provide feedback, contact [Microsoft Graph|Support](https://developer.microsoft.com/graph/support).
