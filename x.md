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
