```PowerShell
$DestPath = "C:\TEMP\Get_Apps_20240428-005.csv" # Change the destination path accordingly!

if (!(Get-Module -ListAvailable -Name MicrosoftPowerBIMgmt)) {
    Write-Host "Module does not exist, installing the module MicrosoftPowerBIMgmt..."
    Install-Module -Name MicrosoftPowerBIMgmt -AllowClobber -Force
}

Connect-PowerBIServiceAccount # Connect to the Power BI service

$response = Invoke-PowerBIRestMethod -Url 'apps' -Method Get
### Ref1 : https://learn.microsoft.com/en-us/powershell/module/microsoftpowerbimgmt.profile/invoke-powerbirestmethod?view=powerbi-ps
### Ref2 : https://learn.microsoft.com/en-us/rest/api/power-bi/apps/get-apps

$apps = $response | ConvertFrom-Json # Convert the response to a PowerShell object

# Loop through each app and each user, outputting a custom object for each user
$apps.value | ForEach-Object {
    $app = $_

		# Create a PSCustomObject for each app
		$appDetails = [PSCustomObject]@{
			"ID" = $app.id
			"Description" = $app.description
			"Name" = $app.name
			"PublishedBy" = $app.publishedBy
			"LastUpdate" = $app.lastUpdate
			"WorkspaceId" = $app.workspaceId
			"Users" = $app.users -join ', '
		}

		# Output the custom object
		$appDetails
} | Sort-Object "LastUpdate" | Export-Csv -Path $DestPath -NoTypeInformation

```
