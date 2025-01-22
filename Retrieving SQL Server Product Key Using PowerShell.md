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

To make the script more dynamic, we updated it to automatically detect the installed SQL Server instances and their versions. Below is the updated script:

```powershell
function GetSqlServerProductKey {
    $localmachine = [Microsoft.Win32.RegistryHive]::LocalMachine
    $defaultview = [Microsoft.Win32.RegistryView]::Default
    $reg = [Microsoft.Win32.RegistryKey]::OpenBaseKey($localmachine, $defaultview)
    $instancesKey = "SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL"
    $instances = $reg.OpenSubKey($instancesKey).GetValueNames()

    foreach ($instance in $instances) {
        $versionKey = "SOFTWARE\Microsoft\Microsoft SQL Server\$instance\Setup"
        $encodedData = $reg.OpenSubKey($versionKey).GetValue("DigitalProductID")
        $reg.Close()

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

        Write-Output "Instance: $instance, Product Key: $productKey"
    }
}

GetSqlServerProductKey
```

### Conclusion

This script will loop through all SQL Server instances on the machine, retrieve their product keys, and print them out. This approach ensures that the script is adaptable to different SQL Server versions and instances.
