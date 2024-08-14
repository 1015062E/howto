<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

Change below registry values to prevent Power BI Report Server from sending requests https://eastus-8.in.applicationinsights.azure.com//v2/track (NOTE: Need to **restart** the computer to make the change take effect)

```ini
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\PBIRS\CPE]
"CustomerFeedback"=dword:00000000
"EnableErrorReporting"=dword:00000000
"ErrorDumpDir"="C:\\Program Files\\Microsoft Power BI Report Server\\PBIRS\\LogFiles"
```

Before  : 
![image](https://github.com/user-attachments/assets/aebfdd77-f519-4d0a-bfba-77e71c64fb7e)


After : 
![image](https://github.com/user-attachments/assets/6f2b6524-85ce-43b8-b134-7dbda561be3a)
