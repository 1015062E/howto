<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>


Change supported authentication types for the Reporting Services(or Report Server) to below.

[Configure Windows authentication on the report server](https://learn.microsoft.com/en-us/sql/reporting-services/security/configure-windows-authentication-on-the-report-server?view=sql-server-ver16)

```
<AuthenticationTypes>
    <RSWindowsNegotiate/>
    <RSWindowsNTLM/>
</AuthenticationTypes>
```

Then : 
<br>![image](https://github.com/user-attachments/assets/694b839b-629a-46fd-9a47-dd38357e0535)
<br>![image](https://github.com/user-attachments/assets/4ccde708-5977-4998-989d-d0d8ad30761c)
<br>![image](https://github.com/user-attachments/assets/35ff0698-88da-4bb8-9086-b7b5b4133baf)
<br>![image](https://github.com/user-attachments/assets/90f48b75-ed8e-4fea-ae76-6980426b9756)

## BTW, Alternatively if you want to make above changes via GPO for all your computers in a specific domain: 
### Follow these steps to add your website `http(s)://xxx.com/Reports` to the Trusted Sites Zone using Group Policy:
1. **Open Group Policy Management Console (GPMC)**: Press `Win + R`, type `gpmc.msc`, and press Enter.
2. **Create or Edit a GPO**: Right-click on the domain or organizational unit (OU) where you want to apply the policy. Select "Create a GPO in this domain, and Link it here..." or choose an existing GPO and select "Edit".
3. **Navigate to the Policy Setting**: Go to `User Configuration` > `Policies` > `Administrative Templates` > `Windows Components` > `Internet Explorer` > `Internet Control Panel` > `Security Page`.
4. **Configure Site to Zone Assignment List**: Double-click on "Site to Zone Assignment List". Enable the policy and click "Show...". In the "Value name" column, enter `http(s)://xxx.com/Reports`. In the "Value" column, enter `2` (which corresponds to the Trusted Sites zone).
  <br>![image](https://github.com/user-attachments/assets/55332ee8-8acf-4bc3-9ae1-71acca0d3344)

5. **Apply and Update Group Policy**: Click "OK" to save the settings. Close the Group Policy Management Editor. On the client machines, run `gpupdate /force` to apply the new policy settings.

### To configure user authentication in trusted sites to "Automatic logon with current username and password" using Group Policy:
1. **Open Group Policy Editor**: Press `Win + R`, type `gpmc.msc`, and press Enter.
2. **Navigate to the Policy Setting**: Go to `User Configuration` > `Policies` > `Administrative Templates` > `Windows Components` > `Internet Explorer` > `Internet Control Panel` > `Security Page` > `Trusted Sites Zone`.
3. **Set Logon Options**: Double-click on "Logon options" and set it to "Automatic logon with current username and password".
4. **Apply the Policy on Client Machines**: Run `gpupdate /force` on the client machines to apply the new policy settings.

![image](https://github.com/user-attachments/assets/08195ca1-ffdc-4fb1-b40c-1a60c40f6170)

---

https://learn.microsoft.com/en-us/previous-versions/troubleshoot/browsers/security-privacy/ie-security-zones-registry-entries

```
HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\CurrentVersion\Internet Settings\Zones\1
Zones\1  -->  Local Intranet
Key:  1A00   User Authentication: Logon 
Value :  10000

Value       Setting
---------------------------------------------------------------
0x00000000  Automatically logon with current username and password
0x00010000  Prompt for user name and password
0x00020000  Automatic logon only in the Intranet zone
0x00030000  Anonymous logon
```
