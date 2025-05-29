
<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

**Disclaimer**: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

## Power BI Desktop AutoRecovery and Backup File Locations

When working with Power BI Desktop, unexpected crashes or application exits can lead to data loss if the `.pbix` file is not manually saved. However, Power BI does implement an **AutoRecovery** feature that attempts to preserve work-in-progress files in specific system directories.

This blog post outlines where these files are typically saved depending on your version of Power BI Desktop (MSI vs. Store App), and how you or a user can potentially recover lost work.

---

### Why This Matters

Users often report that their `.pbix` files become corrupted or inaccessible after an unexpected shutdown or crash. If AutoRecovery was enabled and functioning properly, there may be a recoverable backup available on disk.

---

### Understanding the Installation Types

Power BI Desktop can be installed in two main ways:

1. **MSI Installer Version** – installed via .msi package (e.g., from the Microsoft website)
2. **Microsoft Store App Version** – installed via the Microsoft Store

Each version stores its temporary AutoRecovery and backup files in different locations.

---

### Known AutoRecovery and TempSave Paths

Below are all the known paths where Power BI Desktop might store temporary backup files:

#### For MSI Version:

```plaintext
%LocalAppData%\Microsoft\Power BI Desktop\TempSaves
````
```plaintext
%LocalAppData%\Microsoft\Power BI Desktop\AutoRecovery
````

#### For Microsoft Store App Version:

```plaintext
%LocalAppData%\Microsoft\Power BI Desktop Store App\TempSaves
```
```plaintext
%LocalAppData%\Microsoft\Power BI Desktop Store App\AutoRecovery
```

#### Additional User Profile Based Paths (less common, but possible):

```plaintext
%USERPROFILE%\Microsoft\Power BI Desktop\TempSaves
%USERPROFILE%\Microsoft\Power BI Desktop\AutoRecovery
%USERPROFILE%\Microsoft\Power BI Desktop Store App\TempSaves
%USERPROFILE%\Microsoft\Power BI Desktop Store App\AutoRecovery
```

---

### How to Attempt Recovery

1. **Navigate to each path above** in order of likelihood.
2. **Sort files by date modified** to find the most recent ones.
3. Look for `.pbix` files, often named with prefixes like:

   * `AutoRecovery_<originalname>_<timestamp>.pbix`
4. **Copy the file** to a safe location like your Desktop.
5. Try opening it with Power BI Desktop.

---

### PowerShell Snippet to Search Quickly

If you're not sure where the files might be hiding, run this PowerShell command:

```powershell
Get-ChildItem -Path "$env:USERPROFILE\Microsoft*" -Recurse -Include *.pbix -ErrorAction SilentlyContinue

Get-ChildItem -Path "$env:LocalAppData\Microsoft*" -Recurse -Include *.pbix -ErrorAction SilentlyContinue

```

This will recursively search for `.pbix` files under folders starting with `Microsoft` in your profile directory.

---

### Best Practices for Preventing Data Loss

* Save your file frequently (Ctrl + S).
* Consider versioning manually by appending dates to file names.
* Use OneDrive or another cloud backup solution.
* Make sure AutoRecovery is enabled (it is by default).

---

### Summary

Power BI Desktop does include AutoRecovery features that can help mitigate the impact of unexpected application crashes. By knowing where to look, users may be able to recover their work without needing to start over.

Be proactive: back up your work and understand where Power BI stores its safety nets.
