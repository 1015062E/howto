### Follow these simple steps to find out the version of your Power BI Desktop:
1. Open **Power BI Desktop**.
2. Click on the **File** menu located at the top left corner of the application window.
3. From the dropdown menu, select **About** at the bottom left.
4. A dialog box will appear displaying various information about Power BI Desktop, including the **version number**.
   <br><img width="368" alt="image" src="https://github.com/1015062E/howto/assets/160798406/cc270036-5f0c-44b7-be40-07d3ce136efb">

### Or run PowerShell command : 
```PowerShell
Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*' | Where-Object { $_.DisplayName -like "Microsoft Power BI Desktop*" } | Select-Object DisplayName, DisplayVersion
```
   ![image](https://github.com/user-attachments/assets/d3f1288c-e181-4ff7-8753-a1948533573f)


```PowerShell
Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*' | Where-Object { $_.DisplayName -eq "Microsoft Power BI Desktop (x64)" } | Select-Object DisplayName, DisplayVersion
```
   ![image](https://github.com/user-attachments/assets/0e6a2a48-5ce0-437a-9524-0749219bd4f6)
