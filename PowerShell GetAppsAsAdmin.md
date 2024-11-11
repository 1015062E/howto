<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

Before you begin, ensure you have the `MicrosoftPowerBIMgmt` module installed. If not, the script will handle the installation for you. Here's the PowerShell script to export the Power BI apps data to a .csv file:

```powershell
$DestPath = "C:\temp\GetAppsAsAdmin.csv" # Change the destination path accordingly!

if (!(Get-Module -ListAvailable -Name MicrosoftPowerBIMgmt)) {
    Write-Host "Module does not exist, installing the module MicrosoftPowerBIMgmt..."
    Install-Module -Name MicrosoftPowerBIMgmt -AllowClobber -Force
}

Connect-PowerBIServiceAccount # Connect to the Power BI service

$response = Invoke-PowerBIRestMethod -Url 'https://api.powerbi.com/v1.0/myorg/admin/apps?$top=1000' -Method Get

$apps = $response | ConvertFrom-Json # Convert the response to a PowerShell object

# Loop through each app and output a custom object for each app
$apps.value | ForEach-Object {
    $app = $_

    # Create a PSCustomObject for each app
    $appDetails = [PSCustomObject]@{
        "ID" = $app.id
        "Name" = $app.name
        "PublishedBy" = $app.publishedBy
        "LastUpdate" = $app.lastUpdate
        "WorkspaceId" = $app.workspaceId
        "Description" = $app.description
    }

    # Output the custom object
    $appDetails
} | Sort-Object "LastUpdate" | Export-Csv -Path $DestPath -NoTypeInformation
```
