<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

Before running the script, ensure that the account used to log in via the upcoming popup window has either the `Tenant.Read.All` or `Tenant.ReadWrite.All` role. This is necessary to retrieve the required information. Without these roles, you may encounter an "unauthorized" error when the script runs.

Please note that this script does not include `GroupType=Personal`. That is a special type of workspace intended for SharePoint list and OneDrive integration. This script is designed to retrieve data for `GroupType=PersonalGroup`, also known as "My workspace" or personal workspace.

If you're interested in a PowerShell script with similar functionality for a normal/collaborative workspace (`GroupType=Workspace`), please check out another post on my GitHub.

```PowerShell
$DestPath = "C:\TEMP\PersonalWorkspace_Details_20240422-003.csv" # Change the destination path accordingly!

if (!(Get-Module -ListAvailable -Name MicrosoftPowerBIMgmt)) {
    Write-Host "Module does not exist, installing the module MicrosoftPowerBIMgmt..."
    Install-Module -Name MicrosoftPowerBIMgmt -AllowClobber -Force
}

# Connect to the Power BI service
Connect-PowerBIServiceAccount

# Get all workspaces(type=PersonalGroup)
$workspaces = Get-PowerBIWorkspace -Scope Organization -Include All -All | Where-Object {$_.Type -eq "PersonalGroup"}

# Loop through each workspace and each user, outputting a custom object for each user
$workspaces | ForEach-Object {
    $workspace = $_
    $workspace.Users | ForEach-Object {
        [PSCustomObject]@{
            "Workspace Type" = $workspace.Type
            "Workspace ID"   = $workspace.Id
            "Workspace Name" = $workspace.Name
            "Principal Type" = $_.PrincipalType
            "Role"           = $_.AccessRight
            "Display Name"   = $_.Identifier
            "Email Address"  = $_.Identifier
        }
    }
} | Sort-Object "Workspace Name" | Export-Csv -Path $DestPath -NoTypeInformation

```

References : 
<br>https://learn.microsoft.com/en-us/powershell/module/microsoftpowerbimgmt.workspaces/get-powerbiworkspace?view=powerbi-ps
<br>https://learn.microsoft.com/en-us/rest/api/power-bi/admin/groups-get-groups-as-admin
