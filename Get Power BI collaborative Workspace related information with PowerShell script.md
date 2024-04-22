

<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

Before running the script, ensure that the account used to log in via the upcoming popup window has either the `Tenant.Read.All` or `Tenant.ReadWrite.All` role. This is necessary to retrieve the required information. Without these roles, you may encounter an "unauthorized" error when the script runs.

This script is designed to retrieve data for `GroupType=Workspace`, shared workspace or simple workspace used to share content with other users in the organization, aka collaborative workspace.


```powershell
$DestPath = "C:\TEMP\Workspace_Details_20240422.csv" # Change the destination path accordingly!

if (!(Get-Module -ListAvailable -Name MicrosoftPowerBIMgmt)) {
    Write-Host "Module does not exist, installing the module MicrosoftPowerBIMgmt..."
    Install-Module -Name MicrosoftPowerBIMgmt -AllowClobber -Force
}

# Connect to the Power BI service
Connect-PowerBIServiceAccount

$authHeader = Get-PowerBIAccessToken

# Get all workspaces(type=Workspace)
$workspaces = Get-PowerBIWorkspace -Scope Organization -Include All -All | Where-Object {$_.Type -eq "Workspace"}

# Loop through each workspace, outputting a custom object for each user
$workspaces | ForEach-Object {
    $workspace = $_
    
    # Get all users for the current workspace
    $users = Invoke-RestMethod -Uri "https://api.powerbi.com/v1.0/myorg/admin/groups/$($workspace.Id)/users" -Headers $authHeader

    $users.value | ForEach-Object {
        [PSCustomObject]@{
            "Workspace Type" = $workspace.Type
            "Workspace ID"   = $workspace.Id
            "Workspace Name" = $workspace.Name
            "Principal Type" = $_.principalType
            "Role"           = $_.groupUserAccessRight
            "Display Name"   = $_.displayName
            "Email Address"  = $(if (![string]::IsNullOrEmpty($_.emailAddress)) { $_.emailAddress } else { $_.identifier })
        }
    }
} | Sort-Object "Workspace Name" | Export-Csv -Path $DestPath -NoTypeInformation
```

References : 
<br>https://learn.microsoft.com/en-us/powershell/module/microsoftpowerbimgmt.workspaces/get-powerbiworkspace?view=powerbi-ps
<br>https://learn.microsoft.com/en-us/rest/api/power-bi/admin/groups-get-groups-as-admin
