<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

## Enabling Large Semantic Model Storage Format for a specific dataset Using PowerShell

### Introduction

In this blog post, we will explore how to enable the large semantic model storage format for Power BI datasets using PowerShell. We will cover the installation and import of the necessary PowerShell module, connecting to the Power BI service, and performing operations on a dataset, such as retrieving storage usage and changing the storage mode to support large semantic models.

### Prerequisites

Before we begin, ensure you have the following:
- PowerShell installed on your machine.
- Appropriate permissions to access and manage Power BI datasets.
- The `MicrosoftPowerBIMgmt` module installed.

### Step-by-Step Guide

#### 1. Check and Install the Power BI Management Module

First, we need to check if the `MicrosoftPowerBIMgmt` module is installed. If it is not, we will install it.

```powershell
if (!(Get-Module -ListAvailable -Name MicrosoftPowerBIMgmt)) {
    Write-Host "Module does not exist, installing the module MicrosoftPowerBIMgmt..."
    Install-Module -Name MicrosoftPowerBIMgmt -AllowClobber -Force
}
```

#### 2. Import the Power BI Management Module

Next, we import the `MicrosoftPowerBIMgmt` module to make its cmdlets available for use.

```powershell
Import-Module MicrosoftPowerBIMgmt
```

#### 3. Connect to the Power BI Service Account

We then connect to the Power BI service account. This will prompt you to sign in.

```powershell
Connect-PowerBIServiceAccount
```

#### 4. Retrieve Actual Storage Usage of a Dataset

To retrieve the actual storage usage of a specific dataset, use the following command. Replace `DATASET_ID` with the actual dataset ID.

```powershell
(Get-PowerBIDataset -Scope Organization -Id "DATASET_ID" -Include actualStorage).ActualStorage
```
![image](https://github.com/user-attachments/assets/2f21f187-7d12-449a-b094-4e5047dc8320)

#### 5. Set the Storage Mode to PremiumFiles

To enable the large semantic model storage format, we need to change the storage mode of the dataset to `PremiumFiles`. Use the following command and replace `DATASET_ID` with the actual dataset ID.

```powershell
Set-PowerBIDataset -Id "DATASET_ID" -TargetStorageMode PremiumFiles
```

#### 6. Verify the Storage Mode Change

Finally, retrieve the actual storage usage again to verify that the storage mode has been changed.

```powershell
(Get-PowerBIDataset -Scope Organization -Id "DATASET_ID" -Include actualStorage).ActualStorage
```
![image](https://github.com/user-attachments/assets/3f237c57-cda6-4013-8b1a-9d7e7f7c3b90)

### Example Output

Here is an example of the output you might see when running these commands:

```plaintext
Environment : Public
TenantId    : <TENANT_ID>
UserName    : <USER_EMAIL>

Id                                   StorageMode
--                                   -----------
<DATASET_ID>                         Abf

Id                                   StorageMode
--                                   -----------
<DATASET_ID>                         PremiumFiles
```

### Conclusion

By following these steps, you can enable the large semantic model storage format for Power BI datasets using PowerShell. This approach helps streamline dataset management tasks and ensures efficient use of Power BI resources.

<br>https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-large-models#enable-with-powershell
<br>https://learn.microsoft.com/en-us/powershell/module/microsoftpowerbimgmt.data/set-powerbidataset?view=powerbi-ps
<br>https://learn.microsoft.com/en-us/powershell/module/microsoftpowerbimgmt.data/get-powerbidataset?view=powerbi-ps
<br>https://learn.microsoft.com/en-us/rest/api/power-bi/datasets/update-dataset-in-group
<br>https://learn.microsoft.com/en-us/rest/api/power-bi/datasets/get-datasets-in-group

---
```PowerShell
if (!(Get-Module -ListAvailable -Name MicrosoftPowerBIMgmt)) {
    Write-Host "Module does not exist, installing the module MicrosoftPowerBIMgmt..."
    Install-Module -Name MicrosoftPowerBIMgmt -AllowClobber -Force
}

# Import the required module
Import-Module MicrosoftPowerBIMgmt

# Connect to the Power BI service account
Connect-PowerBIServiceAccount

(Get-PowerBIDataset -Scope Organization -Id "<DATASET_ID>" -Include actualStorage).ActualStorage

Set-PowerBIDataset -Id "<DATASET_ID>" -TargetStorageMode PremiumFiles

(Get-PowerBIDataset -Scope Organization -Id "<DATASET_ID>" -Include actualStorage).ActualStorage
```

```cmd
PS C:\Users\Administrator> if (!(Get-Module -ListAvailable -Name MicrosoftPowerBIMgmt)) {
>>     Write-Host "Module does not exist, installing the module MicrosoftPowerBIMgmt..."
>>     Install-Module -Name MicrosoftPowerBIMgmt -AllowClobber -Force
>> }
PS C:\Users\Administrator>
PS C:\Users\Administrator> # Import the required module
PS C:\Users\Administrator> Import-Module MicrosoftPowerBIMgmt
PS C:\Users\Administrator>
PS C:\Users\Administrator> # Connect to the Power BI service account
PS C:\Users\Administrator> Connect-PowerBIServiceAccount


Environment : Public
TenantId    : <TenantId>
UserName    : <Email>



PS C:\Users\Administrator>
PS C:\Users\Administrator> (Get-PowerBIDataset -Scope Organization -Id "<DATASET_ID>" -Include actualStorage).ActualStorage

Id                                   StorageMode
--                                   -----------
<DATASET_ID>         Abf


PS C:\Users\Administrator> Set-PowerBIDataset -Id "<DATASET_ID>" -TargetStorageMode PremiumFiles
PS C:\Users\Administrator> (Get-PowerBIDataset -Scope Organization -Id "<DATASET_ID>" -Include actualStorage).ActualStorage

Id                                    StorageMode
--                                    -----------
<DATASET_ID> PremiumFiles


PS C:\Users\Administrator>
```

---
