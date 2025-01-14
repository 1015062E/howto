<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

This PowerShell script is used to refresh a Power BI dataset. The script uses the Power BI REST API to initiate a dataset refresh.

Prerequisite : [Use Service Principal Authentication for Power BI REST APIs(Deprecated!!!)](https://github.com/1015062E/howto/blob/main/How%20to%20Use%20Service%20Principal%20Authentication%20for%20Power%20BI%20REST%20APIs.md)

Refer to MS doc - [Service principal is an authentication method that can be used to let an Microsoft Entra application access Power BI service content and APIs.](https://learn.microsoft.com/en-us/power-bi/developer/embedded/embed-service-principal?tabs=azure-portal#get-started-with-a-service-principal)

```PowerShell
# Set the tenant ID, client ID, and client secret
$tenantId = "" # Directory (tenant) ID
$clientId = "" # Application (client) ID
$clientSecret = ""
$WORKSPACE_ID = ""
$DATASET_ID = ""

# Set the resource and authority
$resource = "https://analysis.windows.net/powerbi/api"
$authority = "https://login.microsoftonline.com/$tenantId"

# Get the access token
$tokenResponse = Invoke-RestMethod -Method Post -Uri "$authority/oauth2/token" -Body @{
    grant_type = "client_credentials"
    client_id = $clientId
    client_secret = $clientSecret
    resource = $resource
}

# Build the authentication header
$authHeader = @{
    'Content-Type'='application/json'
    'Authorization'= $tokenResponse.token_type + " " + $tokenResponse.access_token
}

# Set the URI, workspace ID, and dataset ID
$uri = "https://api.powerbi.com/v1.0/myorg/groups/$($WORKSPACE_ID)/datasets/$($DATASET_ID)/refreshes"

# Set the notifyOption
$json = '{
    "notifyOption": "NoNotification"
}' | ConvertFrom-Json
$body = $json | ConvertTo-Json

# Call the API to initiate a dataset refresh
Invoke-RestMethod -Uri $uri -Headers $authHeader -body $body -Method POST
```

This script can be used to automate dataset refreshes in Power BI. To use this script, replace `<TENANT_ID>`, `<CLIENT_ID>`, `<CLIENT_SECRET>`, `<WORKSPACE_ID>`, and `<DATASET_ID>` with your own values.

For more information on using the Power BI REST API, you can refer to the [Power BI REST APIs](https://docs.microsoft.com/en-us/rest/api/power-bi/) specifically this API [Datasets - Refresh Dataset In Group](https://learn.microsoft.com/en-us/rest/api/power-bi/datasets/refresh-dataset-in-group)
