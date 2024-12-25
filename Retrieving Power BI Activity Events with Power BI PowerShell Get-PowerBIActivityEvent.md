
<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

[Full Power BI Operation list](https://learn.microsoft.com/en-us/fabric/admin/operation-list) | [Get-PowerBIActivityEvent](https://learn.microsoft.com/en-us/powershell/module/microsoftpowerbimgmt.admin/get-powerbiactivityevent?view=powerbi-ps). Note: Both StartDateTime and EndDateTime should be within the same UTC day.<br>

```powershell
if (!(Get-Module -ListAvailable -Name MicrosoftPowerBIMgmt)) {
    Write-Host "Module does not exist, installing the module MicrosoftPowerBIMgmt..."
    Install-Module -Name MicrosoftPowerBIMgmt -AllowClobber -Force
}

# Import the required module
Import-Module MicrosoftPowerBIMgmt

# Connect to the Power BI service account
Connect-PowerBIServiceAccount

# Set the end date for the log search to the current date and time in UTC
$endDate = (Get-Date).ToUniversalTime()

# Set the start date to the start of the current UTC day
$startDate = Get-Date $endDate.Date

# Format the start and end dates as strings in the 'yyyy-MM-ddTHH:mm:ss' format
$startDateString = $startDate.ToString("yyyy-MM-ddTHH:mm:ss")
$endDateString = $endDate.ToString("yyyy-MM-ddTHH:mm:ss")

# Get the Power BI activity events
$events = Get-PowerBIActivityEvent -StartDateTime $startDateString -EndDateTime $endDateString

# Save the retrieved events
$events | Out-File -FilePath ("C:\PowerBIActivityEvent_" + ($startDate.ToString("yyyyMMdd")) + ".txt")
```

<br>

```powershell
if (!(Get-Module -ListAvailable -Name MicrosoftPowerBIMgmt)) {
    Write-Host "Module does not exist, installing the module MicrosoftPowerBIMgmt..."
    Install-Module -Name MicrosoftPowerBIMgmt -AllowClobber -Force
}

# Import the required module
Import-Module MicrosoftPowerBIMgmt

# Connect to the Power BI service account
Connect-PowerBIServiceAccount

# Initialize an array to hold the output
$output = @()

# Loop over the past 30 days
for ($i=0; $i -le 30; $i++) {
    $start = (Get-Date).AddDays(-$i).ToString("yyyy-MM-ddT00:00:00")
    $end = (Get-Date).AddDays(-$i).ToString("yyyy-MM-ddT23:59:59")

    # Retrieve the activity events for the day and add them to the output array
    $json = Get-PowerBIActivityEvent -StartDateTime $start -EndDateTime $end # -ActivityType "InstallTemplateApp" 

    # Convert the JSON string to a PowerShell object
    $events = $json | ConvertFrom-Json

    # Add the events to the output array
    $output += $events | Select-Object Operation, OrganizationId, UserId, Activity, IsSuccess, RequestId, TemplateAppObjectId, TemplatePackageName, TemplateAppOwnerTenantObjectId, TemplateAppFolderObjectId
}

# Convert the output array to a CSV string
$csv = $output | ConvertTo-Csv -NoTypeInformation

# Remove quotes from the CSV string
$csv = $csv.Replace('"', '')

# Write the CSV string to a file
$csv | Out-File -FilePath "C:\temp\001.csv"
```
