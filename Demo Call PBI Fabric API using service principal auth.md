<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

Demo API:  [Admin API - List Workspaces](https://learn.microsoft.com/en-us/rest/api/fabric/admin/workspaces/list-workspaces?tabs=HTTP)

It's an Admin API, make sure your SP is added to a security group and the group is granted below access in [Admin Portal](https://app.powerbi.com/admin-portal): 
<br>![image](https://github.com/user-attachments/assets/53664599-78ef-4c51-88ff-461fe9ebb63f)



```PowerShell
# Set the tenant ID, client ID, and client secret
$tenantId = ""
$clientId = ""
$clientSecret = ""

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

# Set the URI
$uri = "https://api.fabric.microsoft.com/v1/admin/workspaces"

# Call the API
Invoke-RestMethod -Uri $uri -Headers $authHeader -Method GET
# $output | Out-File -FilePath "C:\output.txt"
```

Sample Output: 
<br><img width="1248" alt="image" src="https://github.com/user-attachments/assets/16cb05fd-7e96-4f50-af09-8f9ed3178778">
