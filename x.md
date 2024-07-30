```PowerShell
#Prerequisites
Install-Module -Name ReportingServicesTools
#Declare SSRS URI
$sourceRsUri = 'http://ServerName/SSRSReportServer/ReportService2010.asmx?wsdl'
#Declare Proxy so we don't need to connect with every command
$proxy = New-RsWebServiceProxy -ReportServerUri $sourceRsUri
#Output ALL Catalog items to file system
Out-RsFolderContent -Proxy $proxy -RsFolder "/FolderName" -Destination 'C:\Temp' -Recurse
```
