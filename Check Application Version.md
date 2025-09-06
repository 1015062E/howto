<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

---

## Windows PowerShell Command to Check Application Version

When working with Windows systems, you might need to check the version of an application installed on your machine. Instead of manually opening file properties in File Explorer, PowerShell provides a quick way to retrieve version details from executable files.

One useful example is checking the version of an installed application such as Adobe Acrobat.

---

### The Command

```powershell
(Get-Item "C:\Program Files\<AppFolder>\<AppName>.exe").VersionInfo | Select-Object FileVersion, ProductVersion
````

> **Note:** Replace `<AppFolder>` and `<AppName>` with the actual folder and executable name of the application you want to inspect.
> Example: For Adobe Acrobat, the path might look like
> `C:\Program Files\Adobe\Acrobat DC\Acrobat\Acrobat.exe`.

Example:
```powershell
((Get-Item "C:\Program Files\Adobe\Acrobat DC\Acrobat\Acrobat.exe").VersionInfo).ProductVersion
````

---

### Step-by-Step Explanation

1. **Get-Item**

   ```powershell
   Get-Item "C:\Program Files\<AppFolder>\<AppName>.exe"
   ```

   Retrieves the file object for the specified executable.

2. **.VersionInfo**

   ```powershell
   (Get-Item ...).VersionInfo
   ```

   Accesses the `VersionInfo` property, which contains detailed metadata about the executable, such as file version, product version, company name, etc.

3. **Select-Object**

   ```powershell
   | Select-Object FileVersion, ProductVersion
   ```

   Filters the output to display only the `FileVersion` and `ProductVersion` properties.

---

### Example Output

```powershell
FileVersion   ProductVersion
-----------   --------------
24.3.20588.0  2024.003.20588
```

* **FileVersion** → The version of the specific executable file.
* **ProductVersion** → The version of the overall product to which the file belongs.

---

### Why Use This Command

* **Quick check**: No need to navigate through file properties in Explorer.
* **Scriptable**: Can be integrated into scripts to automatically audit software versions.
* **Accurate**: Reads directly from the file’s embedded metadata.

---

### Optional: Simplify the Output

If you prefer a cleaner output (just the version number), you can extend the command like this:

```powershell
((Get-Item "C:\Program Files\<AppFolder>\<AppName>.exe").VersionInfo).ProductVersion
```

This will return just the product version as a single string.
