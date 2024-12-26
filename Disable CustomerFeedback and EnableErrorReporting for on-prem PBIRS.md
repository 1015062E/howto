<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>



#### 1.For on-prem Power BI Report Server: Change below registry values to prevent PBIRS from sending requests https://eastus-8.in.applicationinsights.azure.com//v2/track (NOTE: Need to **restart** the computer to make the change take effect)

```ini
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\PBIRS\CPE]
"CustomerFeedback"=dword:00000000
"EnableErrorReporting"=dword:00000000
```

Below is a PowerShell(Open PowerShell as Administrator) script that checks if the key exists and sets the value accordingly:
```PowerShell
# Define the registry path and keys
$regPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\PBIRS\CPE"
$regKeys = @{
    "CustomerFeedback" = 0
    "EnableErrorReporting" = 0
}

# Check if the registry path exists
if (Test-Path $regPath) {
    foreach ($key in $regKeys.Keys) {
        # Check if the value exists
        if (Get-ItemProperty -Path $regPath -Name $key -ErrorAction SilentlyContinue) {
            # Update the value
            Set-ItemProperty -Path $regPath -Name $key -Value $regKeys[$key]
            Write-Output "Updated existing registry key: $key."
        } else {
            # Create the value
            New-ItemProperty -Path $regPath -Name $key -Value $regKeys[$key] -PropertyType DWORD
            Write-Output "Created new registry key: $key."
        }
    }
} else {
    # Create the key and set the values
    New-Item -Path $regPath -Force | Out-Null
    foreach ($key in $regKeys.Keys) {
        New-ItemProperty -Path $regPath -Name $key -Value $regKeys[$key] -PropertyType DWORD
        Write-Output "Created new registry key and value: $key."
    }
}
```

![image](https://github.com/user-attachments/assets/6f2b6524-85ce-43b8-b134-7dbda561be3a)

#### 2.For SSRS 2017 and after(2019, 2022), the registry path is : 

```ini
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\SSRS\CPE]
"CustomerFeedback"=dword:00000000
"EnableErrorReporting"=dword:00000000
```

Below is a PowerShell(Open PowerShell as Administrator) script that checks if the key exists and sets the value accordingly:
```PowerShell
# Define the registry path and keys
$regPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\SSRS\CPE"
$regKeys = @{
    "CustomerFeedback" = 0
    "EnableErrorReporting" = 0
}

# Check if the registry path exists
if (Test-Path $regPath) {
    foreach ($key in $regKeys.Keys) {
        # Check if the value exists
        if (Get-ItemProperty -Path $regPath -Name $key -ErrorAction SilentlyContinue) {
            # Update the value
            Set-ItemProperty -Path $regPath -Name $key -Value $regKeys[$key]
            Write-Output "Updated existing registry key: $key."
        } else {
            # Create the value
            New-ItemProperty -Path $regPath -Name $key -Value $regKeys[$key] -PropertyType DWORD
            Write-Output "Created new registry key: $key."
        }
    }
} else {
    # Create the key and set the values
    New-Item -Path $regPath -Force | Out-Null
    foreach ($key in $regKeys.Keys) {
        New-ItemProperty -Path $regPath -Name $key -Value $regKeys[$key] -PropertyType DWORD
        Write-Output "Created new registry key and value: $key."
    }
}
```

![image](https://github.com/user-attachments/assets/4d1a1bd9-a53a-4c5b-a63c-6279d8238638)

<br>Ref : https://learn.microsoft.com/en-us/sql/sql-server/usage-and-diagnostic-data-configuration-for-sql-server?view=sql-server-ver16
