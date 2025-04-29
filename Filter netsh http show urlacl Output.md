<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

## How to Filter netsh http show urlacl Output by Reserved URL Containing a Specific String

When managing URL reservations for services like **SQL Server Reporting Services (SSRS)** or **Power BI Report Server** on Windows, you might need to filter the `netsh http show urlacl` output to only show entries where the **Reserved URL** contains a specific keyword, such as `"report"`.

This guide explains how to do that properly using PowerShell.

---

### Background

The `netsh http show urlacl` command lists all HTTP URL reservations on a Windows system.  
However, it **does not offer built-in filtering**, and the output is **multi-line** per reservation entry.

A naive approach using text search will match **any line**, not just the Reserved URL, which can cause false positives — for example, if the user account name includes the word "report" but the Reserved URL does not.

**Example scenario:**  
You are only interested in SSRS or Power BI Report Server URL reservations, and you want to filter those where the Reserved URL contains the string "report".

---

### Simple Text Search Approach (Not Precise)

You can use a basic PowerShell command to search for `"Report"` anywhere in the output:

```powershell
netsh http show urlacl | Select-String -Pattern "Report" -Context 2,2
```

- `Select-String` searches the text output for lines containing "Report".
- `-Context 2,2` displays 2 lines before and after each matching line for context.

**⚠ Important Note:**  
This method matches **any occurrence** of "Report", including in the User field or elsewhere.  
It does **not restrict** the match to only the Reserved URL.

---

