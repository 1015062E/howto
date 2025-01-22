<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

## Retrieving SQL Server Product Key Using PowerShell

### Introduction

In this post, we will discuss how to retrieve the product key for SQL Server Reporting Services (SSRS) using a PowerShell script. This script accesses the registry, extracts the `DigitalProductID`, decodes it, and formats it into a readable product key.

### PowerShell Script Overview

The provided PowerShell script performs the following steps:

1. **Registry Access**: Opens the registry key where the SQL Server instance information is stored.
2. **Data Extraction**: Extracts the `DigitalProductID` value.
3. **Decoding**: Decodes the binary data to generate the product key.
4. **Formatting**: Formats the product key into a readable string.

### Dynamic Instance Detection

To make the script more dynamic, we initially attempted to automatically detect the installed SQL Server instances and their versions. However, we encountered issues with the registry path. Therefore, we updated the script to explicitly specify the instance name.

### Updated PowerShell Script

Here is the updated script where you can specify the instance name:

```powershell
function GetSqlServerProductKey($InstanceName) {
    $localmachine = [Microsoft.Win32.RegistryHive]::LocalMachine
    $defaultview = [Microsoft.Win32.RegistryView]::Default
    $reg = [Microsoft.Win32.RegistryKey]::OpenBaseKey($localmachine, $defaultview)
    $versionKey = "SOFTWARE\Microsoft\Microsoft SQL Server\$InstanceName\Setup"
    $setupKey = $reg.OpenSubKey($versionKey)

    if ($setupKey -eq $null) {
        Write-Output "Setup key not found for instance: $InstanceName"
        return
    }

    $encodedData = $setupKey.GetValue("DigitalProductID")
    $setupKey.Close()

    try {
        $binArray = ($encodedData)[0..66]
        $productKey = $null

        $charsArray = "B", "C", "D", "F", "G", "H", "J", "K", "M", "P", "Q", "R", "T", "V", "W", "X", "Y", "2", "3", "4", "6", "7", "8", "9"

        $isNKey = ([math]::truncate($binArray[14] / 0x6) -band 0x1) -ne 0
        if ($isNKey) {
            $binArray[14] = $binArray[14] -band 0xF7
        }

        $last = 0

        for ($i = 24; $i -ge 0; $i--) {
            $k = 0
            for ($j = 14; $j -ge 0; $j--) {
                $k = $k * 256 -bxor $binArray[$j]
                $binArray[$j] = [math]::truncate($k / 24)
                $k = $k % 24
            }
            $productKey = $charsArray[$k] + $productKey
            $last = $k
        }

        if ($isNKey) {
            $part1 = $productKey.Substring(1, $last)
            $part2 = $productKey.Substring(1, $productKey.Length - 1)
            if ($last -eq 0) {
                $productKey = "N" + $part2
            } else {
                $productKey = $part2.Insert($part2.IndexOf($part1) + $part1.Length, "N")
            }
        }

        $productKey = $productKey.Insert(20, "-").Insert(15, "-").Insert(10, "-").Insert(5, "-")
    } catch {
        $productKey = "Cannot decode product key."
    }

    Write-Output "Instance: $InstanceName, Product Key: $productKey"
}

# Example usage
GetSqlServerProductKey -InstanceName "MSSQL16.InstanceName"
```

Replace `"MSSQL16.InstanceName"` with the actual instance name of your SQL Server 2022 installation. This script will now target the specified instance directly.

### Conclusion

This script allows you to retrieve the product key for a specified SQL Server instance. Ensure you replace the placeholder instance name with the actual instance name of your SQL Server installation.
