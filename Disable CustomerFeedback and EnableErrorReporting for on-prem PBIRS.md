<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

### Change below registry values to prevent Power BI Report Server from sending requests https://eastus-8.in.applicationinsights.azure.com//v2/track (NOTE: Need to **restart** the computer to make the change take effect)

```ini
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\PBIRS\CPE]
"CustomerFeedback"=dword:00000000
"EnableErrorReporting"=dword:00000000
```

Before  : 
![image](https://github.com/user-attachments/assets/aebfdd77-f519-4d0a-bfba-77e71c64fb7e)


After : 
![image](https://github.com/user-attachments/assets/6f2b6524-85ce-43b8-b134-7dbda561be3a)

### For SSRS 2017 and after(2019, 2022), the registry path is : Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\SSRS\CPE
![image](https://github.com/user-attachments/assets/4d1a1bd9-a53a-4c5b-a63c-6279d8238638)

```ini
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\SSRS\CPE]
"CustomerFeedback"=dword:00000000
"EnableErrorReporting"=dword:00000000
"ErrorDumpDir"="C:\\Program Files\\Microsoft SQL Server Reporting Services\\SSRS\\LogFiles"
```
