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
![image](https://github.com/user-attachments/assets/35ff0698-88da-4bb8-9086-b7b5b4133baf)

Then : 
<br>![image](https://github.com/user-attachments/assets/694b839b-629a-46fd-9a47-dd38357e0535)
<br>![image](https://github.com/user-attachments/assets/4ccde708-5977-4998-989d-d0d8ad30761c)
<br>![image](https://github.com/user-attachments/assets/43a629fb-ef80-41f7-b6aa-aaa4f72d788d)
<br>![image](https://github.com/user-attachments/assets/90f48b75-ed8e-4fea-ae76-6980426b9756)

BTW, you can also follow steps below to configure user authentication in trusted sites to "Automatic logon with current username and password" using Group Policy:
1. **Open Group Policy Editor**: Press `Win + R`, type `gpmc.msc`, and press Enter.
2. **Navigate to the Policy Setting**: Go to `User Configuration` > `Policies` > `Administrative Templates` > `Windows Components` > `Internet Explorer` > `Internet Control Panel` > `Security Page` > `Trusted Sites Zone`.
3. **Set Logon Options**: Double-click on "Logon options" and set it to "Automatic logon with current username and password".
4. **Apply the Policy on Client Machines**: Run `gpupdate /force` on the client machines to apply the new policy settings.

![image](https://github.com/user-attachments/assets/08195ca1-ffdc-4fb1-b40c-1a60c40f6170)

