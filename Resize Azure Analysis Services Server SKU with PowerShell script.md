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
<br>https://learn.microsoft.com/en-us/azure/analysis-services/analysis-services-overview#availability-by-region | Azure Analysis Services is supported in regions throughout the world. Supported plans and query replica availability depend on the region you choose. Plan and query replica availability can change depending on need and available resources for each region.
<br>https://learn.microsoft.com/en-us/powershell/module/az.analysisservices/set-azanalysisservicesserver?view=azps-11.5.0 | Set-AzAnalysisServicesServer

>**Note:**
>Azure Analysis Services is available in Developer, Basic, and Standard tiers. Within each tier, plan costs vary according to processing power, Query Processing Units (QPUs), and memory size. When you create a server, you select a plan within a tier. You can change plans up or down within the same tier, or upgrade to a higher tier, but you can't downgrade from a higher tier to a lower tier.
