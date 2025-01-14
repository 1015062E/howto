<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>


Please follow the steps below to resolve the authentication issue related to the loopback check when accessing the Reporting Services URL.  

## 1.Set the DisableStrictNameChecking registry entry to 1. 
```ini
Registry location: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters
DWORD name: DisableStrictNameChecking
DWORD value: 1
```

Below is a PowerShell(Open PowerShell as Administrator) script that checks if the key exists and sets the value accordingly:
    
    # Define the registry path and key
    $regPath = "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters"
    $regName = "DisableStrictNameChecking"
    $regValue = 1
    
    # Check if the key exists
    if (Test-Path $regPath) {
        # Check if the value exists
        if (Get-ItemProperty -Path $regPath -Name $regName -ErrorAction SilentlyContinue) {
            # Update the value
            Set-ItemProperty -Path $regPath -Name $regName -Value $regValue
            Write-Output "Updated existing registry key."
        } else {
            # Create the value
            New-ItemProperty -Path $regPath -Name $regName -Value $regValue -PropertyType DWORD
            Write-Output "Created new registry key."
        }
    } else {
        # Create the key and set the value
        New-Item -Path $regPath -Force | Out-Null
        New-ItemProperty -Path $regPath -Name $regName -Value $regValue -PropertyType DWORD
        Write-Output "Created new registry key and value."
    }
    
## 2.Then use either of the following methods, as appropriate for your situation.

### [Method1 (Recommended): Create Local Security Authority Host Names for NTLM Authentication](https://learn.microsoft.com/en-us/troubleshoot/windows-server/networking/accessing-server-locally-with-fqdn-cname-alias-denied#method-1-recommended-create-the-local-security-authority-host-names-that-can-be-referenced-in-a-ntlm-authentication-request)

1. Click **Windows Start**, click **Run**, type `regedit`, and then click **OK**.
2. Locate and then click the following registry subkey: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\MSV1_0`.
3. Right-click `MSV1_0`, point to **New**, and then click **Multi-String Value**.
4. In the **Name** column, type `BackConnectionHostNames`, and then press **ENTER**.
5. Right-click `BackConnectionHostNames`, and then click **Modify**.
6. In the **Value data** box, type the CNAME or the DNS alias used for the local shares on the computer, and then click **OK**. (1.Do not contain leading or trailing spaces!  2.Each host name should be on a new line.  3.Below values are samples, you need to change these values accordingly.)
    ```
    servername
    servername.domain.com
    virtualname
    virtualname.domain.com
    ```
7. Exit Registry Editor, restart the client computer, and then test if the issue persists.

### [Method2: Disable the Authentication Loopback Check](https://learn.microsoft.com/en-us/troubleshoot/windows-server/networking/accessing-server-locally-with-fqdn-cname-alias-denied#method-2-disable-the-authentication-loopback-check)

Setting the `DisableLoopbackCheck` registry entry in the `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa` registry subkey to `1`. Follow these steps on the client computer:

1. Click **Windows Start**, click **Run**, type `regedit`, and then click **OK**.
2. Locate and then click the following registry subkey: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa`.
3. Right-click `Lsa`, point to **New**, and then click **DWORD Value**.
4. Type `DisableLoopbackCheck`, and then press **ENTER**.
5. Right-click `DisableLoopbackCheck`, and then click **Modify**.
6. In the **Value data** box, type `1`, and then click **OK**.
7. Exit **Registry Editor**.
8. **Restart** the computer and test if the issue still persits. (You must restart the computer for this change to take effect.)

    Below is a PowerShell(Open PowerShell as Administrator) script that checks if the key exists and sets the value accordingly:
    
    ```powershell
    # Define the registry path and key
    $regPath = "HKLM:\SYSTEM\CurrentControlSet\Control\Lsa"
    $regName = "DisableLoopbackCheck"
    $regValue = 1
    
    # Check if the key exists
    if (Test-Path $regPath) {
        # Check if the value exists
        if (Get-ItemProperty -Path $regPath -Name $regName -ErrorAction SilentlyContinue) {
            # Update the value
            Set-ItemProperty -Path $regPath -Name $regName -Value $regValue
            Write-Output "Updated existing registry key."
        } else {
            # Create the value
            New-ItemProperty -Path $regPath -Name $regName -Value $regValue -PropertyType DWORD
            Write-Output "Created new registry key."
        }
    } else {
        # Create the key and set the value
        New-Item -Path $regPath -Force | Out-Null
        New-ItemProperty -Path $regPath -Name $regName -Value $regValue -PropertyType DWORD
        Write-Output "Created new registry key and value."
    }
    ```

Ref: https://learn.microsoft.com/en-us/troubleshoot/windows-server/networking/accessing-server-locally-with-fqdn-cname-alias-denied

---
### Difference Between FQDN and CNAME

- **FQDN (Fully Qualified Domain Name)**: The complete domain name for a specific computer or host on the internet. Example: `www.example.com`.
- **CNAME (Canonical Name) Record**: A DNS record that maps an alias name to a true (canonical) domain name. Example: `blog.example.com` as a CNAME for `example.com`.

### Why Do We Need CNAME Records?

**Purpose**: CNAME records create aliases for domain names, simplifying DNS management and providing flexibility.

**Use Cases**:
- **Simplified Management**: Update a single A record and have multiple CNAMEs point to it.
- **Multiple Services**: Different services (like `www.example.com` and `ftp.example.com`) can point to the same IP address using CNAMEs.
- **Consistency**: Ensures all related domains point to the same IP address, reducing the risk of errors.

### BackConnectionHostNames Registry and Authentication

**NTLM Authentication**: The `BackConnectionHostNames` registry entry resolves issues with NTLM authentication when accessing a server locally using its FQDN or CNAME alias.

**Kerberos Authentication**: For Kerberos, you need to add Service Principal Names (SPNs) and ensure proper DNS settings. The `BackConnectionHostNames` registry entry does not directly affect Kerberos authentication.

**When to Change**:
- **NTLM**: Change the `BackConnectionHostNames` registry entry when facing authentication issues accessing local resources using FQDN or CNAME.
- **Kerberos**: Ensure SPNs are correctly configured and DNS settings are accurate.

### Local Security Authority (LSA)

**What is LSA?**: The Local Security Authority (LSA) is a component of the Windows operating system that enforces security policies, manages user logins, and handles authentication.

**Why It's Involved**: LSA handles authentication processes, including NTLM and Kerberos. The `BackConnectionHostNames` registry entry helps LSA recognize specific host names during NTLM authentication requests.

**Remote or Domain Security Authority**: In a domain environment, the Domain Controller (DC) performs similar functions for domain-wide authentication and security policies, using the Key Distribution Center (KDC) for Kerberos authentication.

---
