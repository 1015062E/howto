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

### Why This Can Be a Problem

If a URL reservation block looks like this:

```
Reserved URL    : http://+:80/SomeOtherService/
User            : NT SERVICE\PowerBIReportServer
Listen          : Yes
Delegate        : No
Sddl            : (A;;GX;;;S-1-5-80-...)
```

- The Reserved URL **does not** contain "Report".
- The **User account** name does.

In this case, the simple text search will still match, even though the Reserved URL is not relevant.

---

### Correct Approach to Match Only Reserved URL Lines

If you want **precision** — matching only when the **Reserved URL** itself contains "Report" —  
you would need a more advanced parsing method.

Example of the logic:
- Read the `netsh http show urlacl` output line-by-line.
- Look for lines starting with `Reserved URL`.
- Check if the Reserved URL contains `"Report"`.
- If it does, collect and display the whole reservation block.

(Extended script is beyond this scope since you requested focus on the basic command.)

---

### Conclusion

For quick manual filtering, this PowerShell command:

```powershell
netsh http show urlacl | Select-String -Pattern "Report" -Context 2,2
```

is **sufficient** when you are aware of its limitations.  
If you require **strict matching** against Reserved URLs only, additional scripting would be needed.

---

### Practical Use Case

Filtering SSRS or Power BI Report Server URL reservations during troubleshooting or configuration validation can be sped up using this method.  
Just keep in mind the potential for **false positives** based on **user account names** or other fields containing the string `"Report"`.
