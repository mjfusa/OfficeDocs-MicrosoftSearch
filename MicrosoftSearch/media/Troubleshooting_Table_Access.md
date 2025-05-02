## Issue: Missing Access to Certain Tables

**Impact:**  
Without the right access, permissions cannot be granted accurately.

---

## Resolution

### Role Required
- ServiceNow Admin

### Steps to Validate Table Permissions using REST API Explorer:

1. Impersonate the crawling account you have created in your ServiceNow instance.  
   > Ensure the account has the following roles: `rest_api_explorer` and `web_service_admin`.
2. Navigate to:  
   **System Web Services > REST > REST API Explorer**
3. Select one of the tables mentioned in the error message.
4. Set `sysparm_limit` to `10` (to limit results for testing).
5. Click on **Send**.
6. Review the Response:
   - **If you receive a `403 Status Code`** and an error message stating you're not authorized to access the table, follow the [steps here](#) to provide table-level access.
   - **If you receive a `200 Status Code`** but the response body contains empty results (e.g., no fields), this indicates row access exists but field-level access is missing. Follow the [steps here](#) to grant field-level access.

> ⚠️ **Note:** If you do not see the table name in the dropdown, it may indicate lack of access to the table itself.

---

### Alternate Method: Using Browser to Check Access

1. Open an **incognito** browser window.
2. Enter the following URL (replace placeholders appropriately):  
   `https://<instance-url>/api/now/table/<table_name>?sysparm_limit=10`
3. When prompted, log in using the **crawling account's credentials**.
4. Review the response:
   - If there is no response or an error appears, the account likely lacks necessary access.
