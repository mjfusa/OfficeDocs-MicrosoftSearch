---
title: "Troubleshooting the GitLab Microsoft Graph Connector"
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
description: "Troubleshooting the GitLab connectors for Microsoft Search and Microsoft 365 Copilot "
ms.date: 14/02/2025
---

# Troubleshooting the GitLab Microsoft Graph Connector

The following are common errors observed while configuring the connector or during crawling, along with their possible reasons.

| Step | Error Message | Possible Reason(s) |
|:------------ |:------------ |:------------|
| **Test Authentication** | **Having trouble? Try signing in again.** | Incorrect **Client ID** or **Client Secret** was provided. |
| **Test Authentication** | **The account doesn’t have permission to access this data source. Make sure that the application has been granted the correct scopes and the account has access. For more details, refer to: aka.ms/gc-gitlab** | The authentication was successful, but the user lacks the necessary GitLab permissions. Ensure that the **read_api** scope is granted, and the user has access to the selected repositories, issues, and wikis. |
| **Test Authentication** | **Graph Connector Agent associated with the connection is not reachable. Either the agent is not running or app credentials have expired/revoked.** | The on-premises Graph Connector Agent is offline, or the credentials have expired. Verify that the agent is running, has internet access, and the application credentials are active. |
| **Test Authentication** | **An unknown error occurred. Try again after some time. If this error persists, contact support.** | A transient issue or potential code bug. Try again later. If the problem continues, contact support. |
| **Crawl Initialization** | **Failed to connect to GitLab with the provided credentials. Verify that the credentials are correct.** | The authentication details were changed or revoked after setup. Update the credentials in the connector settings. |
| **Crawl Initialization** | **Failed to connect to GitLab. Make sure your GitLab is up and running, and the Graph Connector Agent has network access to the GitLab server. For troubleshooting, refer to: aka.ms/gc-gitlab** | The GitLab server is unreachable due to network issues, incorrect GitLab URL, or firewall restrictions. Ensure GitLab is accessible from the connector. |
| **Item Fetching** | **The crawler account does not have permissions for the item. Check that the crawler account has been granted access to this item in GitLab.** | The crawler lacks read access for the item. Ensure the authentication account has the appropriate repository, issue, or wiki access. |
| **Item Fetching** | **We got Error code - {code}, Error Message - {ReasonPhrase}. If the error persists, contact support.** | A **400 Bad Request** error, likely caused by a malformed request or API issue. |
| **Item Fetching** | **We got Error code - {code}, Error Message - {ReasonPhrase}. The {file/wiki/issue/MR} seems to be already removed from GitLab. Make sure the file exists and try again. If the error persists, contact support.** | A **404 Not Found** error, indicating the item no longer exists in GitLab. Ensure the item is still available. |
| **Item Fetching** | **We got Error code - {code}, Error Message - {ReasonPhrase}. A server-side error occurred while crawling the item. Try recrawling the connection after some time. If the error persists, contact support.** | A **5XX Internal Server Error** from GitLab, likely due to temporary service issues. Try again later. |
| **Item Fetching** | **We got Error code - {code}, Error Message - {ReasonPhrase}. If the error persists, please contact support.** | A **429 Too Many Requests** error, indicating API rate limits were exceeded. Consider increasing the crawl interval or requesting a higher rate limit from GitLab. |

## Next Steps
If the issue persists, verify your configuration settings, authentication credentials, and network connectivity.  
For additional support, visit [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
