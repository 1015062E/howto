**Please refer to this document at your own discretion and understanding of potential risks involved.**

REF : 
<br>https://learn.microsoft.com/en-us/rest/api/power-bi/reports/export-to-file-in-group
<br>https://learn.microsoft.com/en-us/rest/api/power-bi/reports/get-export-to-file-status-in-group
<br>https://learn.microsoft.com/en-us/rest/api/power-bi/reports/get-file-of-export-to-file-in-group


<br>Change the Report ID and Group ID inline, and the ouptput folder path accordingly (by default it's C:\\)
<br>If your report path is https://app.powerbi.com/groups/XXXXX/reports/YYYYY/ReportSectionZZZZZ?experience=power-bi, then XXXXX is your group ID and YYYYY is your report ID. 

```PowerShell
# Import the required module
Import-Module -Name MicrosoftPowerBIMgmt

# Connect to the Power BI service
Connect-PowerBIServiceAccount

$authHeader = Get-PowerBIAccessToken

# Define parameters
$groupId = "XXXXX" ### REPLACE THE VALUE
$reportId = "YYYYY" ### REPLACE THE VALUE


# Define the REST API endpoint for initiating the export
$uriExportTo = "https://api.powerbi.com/v1.0/myorg/groups/$($groupId)/reports/$($reportId)/ExportTo"

# Define the body for the request
$body = @{
    format = "PDF"
}

# Make the POST request to initiate the export
Write-Output ((Get-Date -Format "yyyy-MM-dd HH:mm:ss") + " , Start invoking API $uriExportTo")
$responseExportTo = Invoke-RestMethod -Uri $uriExportTo -Headers $authHeader -Body $body -Method Post

Start-Sleep -s 5  # Sleep 5 seconds

Write-Output "responseExportTo"
$responseExportTo | Format-List *

# Get the export ID from the response
$exportId = $responseExportTo.id

# Define the REST API endpoint for checking the export status
$uriExportStatus = "https://api.powerbi.com/v1.0/myorg/groups/$($groupId)/reports/$($reportId)/exports/$($exportId)"

# Initialize a counter for the loop
$counter = 0

# Check if the request was successful every second for up to 60 seconds
while ($counter -lt 60) {
    Start-Sleep -s 1

    # Make a GET request to check the export status
    $responseExportStatus = Invoke-RestMethod -Uri $uriExportStatus -Headers $authHeader -Method Get

    if ($responseExportStatus.status -eq "Succeeded") { # Download the exported file if export succeeded
        $reportName = $responseExportStatus.reportName -replace ' ', '_'
        $dateTime   = Get-Date -Format "yyyyMMddHHmmss"
        $filePath   = "C:\$($reportName)_$($dateTime)$($responseExportStatus.resourceFileExtension)"

        # Save the content to the file
        $exportedFileContent | Out-File -FilePath $filePath

        Invoke-WebRequest -Uri $responseExportStatus.resourceLocation -Headers $authHeader -OutFile $filePath

        if (Test-Path $filePath) {
            Write-Output ((Get-Date -Format "yyyy-MM-dd HH:mm:ss") + " ,Export Succeeded and saved the file to : $($filePath)")
        } else {
            Write-Output "File not generated yet"
        }
        break
    } elseif ($responseExportStatus.status -eq "Failed") {
        Write-Output "Export failed with status: $($responseExportStatus.status)"
        break
    } else {
        Write-Output "Export status: $($responseExportStatus.status), after checking status for $counter seconds"
    }

    # Increment the counter by 1
    $counter++
}

if ($counter -eq 60) {
    Write-Output "Export did not complete within 60 seconds."
}
```
