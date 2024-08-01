<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

```PowerShell
# Install the required module if it doesn't exist
if (!(Get-Module -ListAvailable -Name MicrosoftPowerBIMgmt)) {
    Write-Host "Module does not exist, installing the moduel MicrosoftPowerBIMgmt......"
    Install-Module -Name MicrosoftPowerBIMgmt -AllowClobber -Force
}

# Connect to the Power BI service
Connect-PowerBIServiceAccount

# Get all workspaces
$workspaces = Get-PowerBIWorkspace -Scope Organization -Type "Workspace" -Include All -All | Where-Object {$_.Type -eq "Workspace"}

$output=@()

# Loop through each workspace
foreach ($workspace in $workspaces) {

    # Loop through each user
    foreach ($user in $workspace.Users) {
        # Create a custom object for the current user
        $userObj = New-Object PSObject -Property @{
            "Workspace ID" = $workspace.Id
            "Workspace Name" = $workspace.Name
            "Role" = $user.AccessRight
            "UserPrincipalName" = $user.UserPrincipalName
            "Identifier" = $user.Identifier
            "Principal Type" = $user.PrincipalType
        }

        # Add the custom object to the output array
        $output += $userObj
    }
}

# Sort the output array by Workspace Name in ascending order, select the properties in the desired order, and export it to a .csv file
$output | Sort-Object "Workspace Name" | Select-Object "Workspace ID", "Workspace Name", "Role", "UserPrincipalName", "Identifier", "Principal Type" | Export-Csv -Path "C:\temp\output003.csv" -NoTypeInformation
```
