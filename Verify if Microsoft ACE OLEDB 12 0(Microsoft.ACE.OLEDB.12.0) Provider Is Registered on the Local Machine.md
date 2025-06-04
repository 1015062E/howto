<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

## How to Verify if Microsoft ACE OLEDB 12 0 Provider Is Registered on the Local Machine

When working with applications like Power BI Desktop, Excel, or legacy systems that connect to Microsoft Access or Excel files via OLEDB, you may encounter errors such as:

```

The 'Microsoft.ACE.OLEDB.12.0' provider is not registered on the local machine.

````

This article walks through several reliable ways to verify whether the `Microsoft.ACE.OLEDB.12.0` provider is installed and properly registered on your local machine.

---

### Understanding the Issue

This provider is required to load data from:

- `.xls`, `.xlsx`, `.xlsb` Excel workbooks
- Access `.mdb`, `.accdb` files

Power BI, when refreshing queries that source from Excel or Access, depends on this provider. If the provider is not properly registered, a data source error will occur.

---

### Step-by-Step: How to Verify the Provider

#### #### Option 1: Check Windows Registry

The most direct method is to check the Windows Registry to see if the provider is registered.

**PowerShell Command (64-bit check):**

```powershell
Get-Item "Registry::HKEY_CLASSES_ROOT\Microsoft.ACE.OLEDB.12.0"
````

If successful, you will see output like:

```plaintext
    Hive: HKEY_CLASSES_ROOT

Name                           Property
----                           --------
Microsoft.ACE.OLEDB.12.0       (default) : Microsoft.ACE.OLEDB.12.0
```

**PowerShell Command (32-bit check):**

```powershell
Get-Item "Registry::HKEY_CLASSES_ROOT\Wow6432Node\Microsoft.ACE.OLEDB.12.0"
```

If this path is not found, it means the 32-bit version is not registered.

---

### Option 2: COM Object Load Test

To verify whether the provider is not only registered but usable, you can attempt to instantiate it using PowerShell:

```powershell
try {
    $conn = New-Object -ComObject ADODB.Connection
    $conn.Provider = "Microsoft.ACE.OLEDB.12.0"
    $conn.Open()
    Write-Host "Provider is installed and working."
    $conn.Close()
} catch {
    Write-Host "Provider test failed: $($_.Exception.Message)"
}
```

> 🔸 If the error message is `Authentication failed`, this usually means the provider was loaded, but no valid connection string or file was supplied. This is acceptable for the purpose of verifying registration.<br>![image](https://github.com/user-attachments/assets/9c54f07f-7979-4e96-83d9-7d8b36a5472e)
<br>![image](https://github.com/user-attachments/assets/f9e2cc5a-ee37-430a-9b46-2b98930f4cf1)


---

### How to Fix If Not Installed

If the provider is not registered, download and install the **Access Database Engine 2016 Redistributable**:

* [Download Link (Microsoft)](https://www.microsoft.com/en-us/download/details.aspx?id=54920)

Install the version that matches your **Power BI Desktop** or **Office** bitness (64-bit vs 32-bit).

Or https://support.microsoft.com/office/download-and-install-microsoft-365-access-runtime-185c5a32-8ba9-491e-ac76-91cbe3ea09c9
---

### Additional Notes

* **Check Power BI Desktop bitness:** Go to `Help > About` in Power BI Desktop.
* **Match bitness:** Ensure your Office, Power BI Desktop, and OLEDB provider are either all 64-bit or all 32-bit.
* **Click-to-Run Office:** If you're using Microsoft 365 (Click-to-Run), the provider may be registered in a virtual registry space inaccessible to non-Office applications like Power BI. Installing the standalone redistributable resolves this.

---

### Troubleshooting Power BI Errors

If you're getting this error in Power BI:

```
An error occurred in the 'QueryName' query. DataSource.Error: Excel Workbook: The 'Microsoft.ACE.OLEDB.12.0' provider is not registered on the local machine.
```

Use the following checklist:

* [ ] Confirm provider is installed (see registry or COM test above).
* [ ] Confirm Power BI Desktop bitness (64-bit or 32-bit).
* [ ] Ensure ACE provider bitness matches Power BI.
* [ ] If on Office 365 Click-to-Run, install standalone provider.
* [ ] Try running Power BI Desktop as Administrator (just to rule out permission issues).

---

### Final Thoughts

Properly verifying and registering the `Microsoft.ACE.OLEDB.12.0` provider is essential for working with Excel or Access data sources in tools like Power BI. These registry and COM test steps provide a reliable way to confirm the provider's availability and avoid confusing runtime errors.
