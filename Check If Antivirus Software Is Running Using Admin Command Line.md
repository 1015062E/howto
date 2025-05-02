<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

## Check If Antivirus Software Is Running Using Admin Command Line

This guide demonstrates how to check whether antivirus (AV) or endpoint protection software is active on a Windows system using the built-in `fltmc` utility via an elevated Command Prompt.

### What Is `fltmc`?

`fltmc` stands for **Filter Manager Control Program**, a command-line tool that lists file system filter drivers currently loaded on a Windows system. Antivirus and security solutions often install such drivers to monitor and protect the file system.

### How To Use `fltmc` to Check for Antivirus

#### Step 1: Open Command Prompt as Administrator

1. Press **Start**, type `cmd`.
2. Right-click on **Command Prompt** and select **Run as administrator**.

#### Step 2: Run the Command

```cmd
fltmc
```

#### Step 3: Review the Output

Sample output:

```
Filter Name                     Num Instances    Altitude    Frame
------------------------------  -------------  ------------  -----
bindflt                                 1       409800         0
MsSecFlt                                5       385600         0
UCPD                                    3       385250.5       0
WdFilter                                3       328010         0
storqosflt                              0       244000         0
wcifs                                   0       189900         0
CldFlt                                  2       180451         0
bfs                                     5       150000         0
FileCrypt                               0       141100         0
luafv                                   1       135000         0
npsvctrig                               1        46000         0
Wof                                     2        40700         0
FileInfo                                3        40500         0
```

---

### Identifying Antivirus-Related Filters

Here are common AV-related filter driver names you might see:

| Filter Driver     | Antivirus Product                   |
|------------------|--------------------------------------|
| `WdFilter`       | Microsoft Defender Antivirus         |
| `MsSecFlt`       | Microsoft Security Services (Defender support) |
| `SymEvent`       | Symantec / Norton                    |
| `mfefirek`       | McAfee                               |
| `csagent`        | CrowdStrike                          |
| `SentinelFilter` | SentinelOne                          |
| `bdvedisk`       | Bitdefender                          |
| `Parity`         | Carbon Black (VMware)                |

In the above example, the presence of both `WdFilter` and `MsSecFlt` confirms that **Microsoft Defender Antivirus** is active and running.

---

### Conclusion

Using `fltmc` is a quick, non-intrusive method to check for active antivirus software on Windows. This can be especially helpful when investigating security posture, assessing baseline configurations, or auditing systems without relying on UI-based tools.

Always validate your findings with IT or endpoint management policies, and cross-reference with `Windows Security` settings or third-party AV dashboards if available.
