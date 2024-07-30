TO DO

<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>


https://github.com/microsoft/ReportingServicesTools

https://github.com/microsoft/ReportingServicesTools/blob/master/ReportingServicesTools/Functions/CatalogItems/Out-RsFolderContent.ps1

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
