<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>


Please follow the steps below to resolve the authentication issue related to the loopback check when accessing the Reporting Services URL.  First, use Method 1 on the Reporting Services server, then restart the server and check if the problem still exists. If the problem persists after implementing Method 1 and restarting the server, please implement Method 2.

### [Method 1 (Recommended): Create Local Security Authority Host Names for NTLM Authentication](link)

1. Click **Windows Start**, click **Run**, type `regedit`, and then click **OK**.
2. Locate and then click the following registry subkey: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\MSV1_0`.
3. Right-click `MSV1_0`, point to **New**, and then click **Multi-String Value**.
4. In the **Name** column, type `BackConnectionHostNames`, and then press **ENTER**.
5. Right-click `BackConnectionHostNames`, and then click **Modify**.
6. In the **Value data** box, type the CNAME or the DNS alias used for the local shares on the computer, and then click **OK**. (Do not contain leading or trailing spaces! Each host name should be on a new line. Below values are samples, you need to change these values accordingly.)
    ```
    servername
    servername.domain.com
    virtualname
    virtualname.domain.com
    ```
7. Exit Registry Editor, restart the **Reporting Services server**, and then test if the issue persists.

### [Method 2: Disable the Authentication Loopback Check](link)

Re-enable the behavior that exists in Windows Server by setting the `DisableLoopbackCheck` registry entry in the `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa` registry subkey to `1`. To set the `DisableLoopbackCheck` registry entry to `1`, follow these steps on the client computer:

1. Click **Windows Start**, click **Run**, type `regedit`, and then click **OK**.
2. Locate and then click the following registry subkey: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa`.
3. Right-click `Lsa`, point to **New**, and then click **DWORD Value**.
4. Type `DisableLoopbackCheck`, and then press **ENTER**.
5. Right-click `DisableLoopbackCheck`, and then click **Modify**.
6. In the **Value data** box, type `1`, and then click **OK**.
7. Exit **Registry Editor**.
8. **Restart** the computer and test if the issue still persits. (You must restart the server for this change to take effect.)
