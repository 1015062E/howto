# How to Get the FQDN of the computer you currently logged on

The Fully Qualified Domain Name (FQDN) of a computer is the complete domain name for a specific computer, consisting of its hostname and the DNS domain name. In this post, we will show you two methods to get the FQDN of your computer: one using the Windows Command Prompt and one using PowerShell.


## Method 0: Using the Windows Command Prompt
```cmd
for /f "tokens=2 delims==" %d in ('wmic computersystem get domain /value ^| findstr /i "Domain"') do @echo %COMPUTERNAME%.%d
```

## Method 1: Using the Windows Command Prompt

You can use the following command in the Windows Command Prompt to get the FQDN of your computer:

```cmd
echo %COMPUTERNAME%.%USERDNSDOMAIN%
```

This command uses the `%COMPUTERNAME%` and `%USERDNSDOMAIN%` environment variables to construct the FQDN of your computer. The `%COMPUTERNAME%` variable contains the hostname of your computer, while the `%USERDNSDOMAIN%` variable contains the DNS domain name of your computer.

Please note that this command may not work if you are not logged into a domain or if your computer is not joined to a domain.

## Method 2: Using PowerShell

You can also use PowerShell to get the FQDN of your computer. Here is the command you can use:

```PowerShell
[System.Net.Dns]::GetHostByName(($env:computerName)).HostName
```

This command uses the `GetHostByName` method of the `System.Net.Dns` class to retrieve the host information for your computer, as specified by the `$env:computerName` environment variable. The `HostName` property of the resulting object contains the FQDN of your computer.
