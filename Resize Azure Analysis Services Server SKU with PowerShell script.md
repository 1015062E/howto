>**Please refer to this document at your own discretion and understanding of potential risks involved.**

```PowerShell
# List of modules to check and install if not available
$modules = @("Az.Accounts", "Az.AnalysisServices")

foreach ($module in $modules) {
    if (!(Get-Module -ListAvailable -Name $module)) {
        Install-Module -Name $module -AllowClobber -Force
    } else {
        Import-Module -Name $module
    }
}

# Login to Azure account
Connect-AzAccount

# Set Subscription context
Set-AzContext -Subscription "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

# Scale up/down your AAS
Set-AzAnalysisServicesServer -ResourceGroupName "xxx" -Name "guoqingsunaas" -Sku "yyy"
```

<br>Reference : 
<brhttps://learn.microsoft.com/en-us/azure/analysis-services/analysis-services-overview#availability-by-region | Azure Analysis Services is supported in regions throughout the world. Supported plans and query replica availability depend on the region you choose. Plan and query replica availability can change depending on need and available resources for each region.
<brhttps://learn.microsoft.com/en-us/powershell/module/az.analysisservices/set-azanalysisservicesserver?view=azps-11.5.0 | Set-AzAnalysisServicesServer
