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
