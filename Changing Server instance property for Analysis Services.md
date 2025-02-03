<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

## Changing Server instance property for Analysis Services

```XML
<Alter AllowCreate="true" ObjectExpansion="ObjectProperties" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">
	<Object />
	<ObjectDefinition>
		<Server xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ddl2="http://schemas.microsoft.com/analysisservices/2003/engine/2" xmlns:ddl2_2="http://schemas.microsoft.com/analysisservices/2003/engine/2/2" xmlns:ddl100_100="http://schemas.microsoft.com/analysisservices/2008/engine/100/100" xmlns:ddl200="http://schemas.microsoft.com/analysisservices/2010/engine/200" xmlns:ddl200_200="http://schemas.microsoft.com/analysisservices/2010/engine/200/200" xmlns:ddl300="http://schemas.microsoft.com/analysisservices/2011/engine/300" xmlns:ddl300_300="http://schemas.microsoft.com/analysisservices/2011/engine/300/300" xmlns:ddl400="http://schemas.microsoft.com/analysisservices/2012/engine/400" xmlns:ddl400_400="http://schemas.microsoft.com/analysisservices/2012/engine/400/400" xmlns:ddl500="http://schemas.microsoft.com/analysisservices/2013/engine/500" xmlns:ddl500_500="http://schemas.microsoft.com/analysisservices/2013/engine/500/500">
			<ID>guoqingsunaas</ID>
			<Name>guoqingsunaas</Name>
			<ServerProperties>
				<ServerProperty>
					<Name>Memory\QueryMemoryLimit</Name>
					<Value>19</Value>
				</ServerProperty>
			</ServerProperties>
		</Server>
	</ObjectDefinition>
</Alter>
```

```PowerShell
# Check if the Az.AnalysisServices module is installed, if not, install it
if (!(Get-Module -ListAvailable -Name Az.AnalysisServices)) {
    Write-Host "Module does not exist, installing the module Az.AnalysisServices..."
    Install-Module -Name Az.AnalysisServices -AllowClobber -Force
}

# Import the necessary module
Import-Module Az.AnalysisServices

# Define the XMLA command
$xmlaCommand = @"
<Alter AllowCreate="true" ObjectExpansion="ObjectProperties" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">
    <Object />
    <ObjectDefinition>
        <Server xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ddl2="http://schemas.microsoft.com/analysisservices/2003/engine/2" xmlns:ddl2_2="http://schemas.microsoft.com/analysisservices/2003/engine/2/2" xmlns:ddl100_100="http://schemas.microsoft.com/analysisservices/2008/engine/100/100" xmlns:ddl200="http://schemas.microsoft.com/analysisservices/2010/engine/200" xmlns:ddl200_200="http://schemas.microsoft.com/analysisservices/2010/engine/200/200" xmlns:ddl300="http://schemas.microsoft.com/analysisservices/2011/engine/300" xmlns:ddl300_300="http://schemas.microsoft.com/analysisservices/2011/engine/300/300" xmlns:ddl400="http://schemas.microsoft.com/analysisservices/2012/engine/400" xmlns:ddl400_400="http://schemas.microsoft.com/analysisservices/2012/engine/400/400" xmlns:ddl500="http://schemas.microsoft.com/analysisservices/2013/engine/500" xmlns:ddl500_500="http://schemas.microsoft.com/analysisservices/2013/engine/500/500">
            <ID>YourASName</ID>
            <Name>YourASName</Name>
            <ServerProperties>
                <ServerProperty>
                    <Name>Memory\QueryMemoryLimit</Name>
                    <Value>19</Value>
                </ServerProperty>
            </ServerProperties>
        </Server>
    </ObjectDefinition>
</Alter>
"@

# Define service principal credentials
$AppId = "<ServicePrincial Application ID>"
$TenantId = "<TenantId>"
$PlainPWord = "<ServicePrincipalSecret>"
$PWord = ConvertTo-SecureString -String $PlainPWord -AsPlainText -Force
$Credential = New-Object -TypeName "System.Management.Automation.PSCredential" -ArgumentList $AppId, $PWord

# Login using service principal
Login-AzureAsAccount -Credential $Credential -ServicePrincipal -TenantId $TenantId -RolloutEnvironment "YourASLocation.asazure.windows.net"

# Execute the XMLA command
Invoke-ASCmd -Server "asazure://YourASLocation.asazure.windows.net/YourASName" -Query $xmlaCommand
```
