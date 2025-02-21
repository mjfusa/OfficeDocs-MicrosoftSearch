--- 
ms.date: 08/28/2024 
title: "Troubleshooting the Veeva Vault PromoMats Microsoft Graph connector" 
ms.author: dannyyao
author: dannyyaou
manager: jecui
audience: Admin 
ms.audience: Admin 
ms.topic: article 
ms.service: mssearch 
ms.localizationpriority: medium 
description: "Troubleshooting the Veeva Vault PromoMats Microsoft Graph connector for Microsoft Search and Microsoft 365 Copilot" 
--- 

# Troubleshooting the Veeva Vault PromoMats Microsoft Graph connector

The following are common errors observed while configuring the connector.

| Error | Description | Resolution|
|:---------|:-------------------------|:------------------------|
| `INVALID_SESSION_ID`    | Authentication session expired or invalid.| Reauthenticate with valid credentials.                             |
| `INSUFFICIENT_ACCESS`   | User lacks permissions to access files.   | Verify user roles and ACLs in Veeva Vault.                   |
| `API_LIMIT_EXCEEDED`    | Too many API requests made in a short period. | Adjust crawl frequency or retry after some time.                  |
| Missing Properties or Documents| Required metadata properties are not enabled. | Ensure metadata properties are enabled in Veeva Vault and test retrieval.|

To view more error types, select the connection and click **error details** > **error code**. For more information, see [Monitor your connections](./manage-connector.md).

### Share your feedback

We value your feedback on the performance of the Veeva Vault - PromoMats Microsoft Graph connector. To help us improve, please take a moment to share your thoughts by using the thumbs-up/thumbs-down icons at the bottom of each response (it only takes a minute). If you're comfortable sharing this data with Microsoft, your feedback plays a key role in improving the service. 

1. When the feedback form opens, please share your comments in the text field about what worked well or what didn’t. **Important**: Include the hashtag #VeevaGC in your feedback.
2. If applicable, add a screenshot.
3. Select `YES` to share your data with Microsoft and `Submit`.

If you have issues or want to provide feedback, contact [Microsoft Graph|Support](https://developer.microsoft.com/en-us/graph/support).
