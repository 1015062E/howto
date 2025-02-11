<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

## How to Collect Power BI Report Builder Logs for Troubleshooting

Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

### Introduction
Collecting logs in Power BI Report Builder is essential for troubleshooting issues effectively. This guide provides step-by-step instructions to enable verbose logging and locate the log files.

### For Power BI Report Builder (Power BI Service)

#### Locate the Configuration File
The configuration file and `Traces` folder are located at:
```
%LocalAppData%\Microsoft\Power BI Report Builder\15.7
```

#### Modify the Logging Configuration
1. Open the `user.config` file.
2. Change the `LoggingTraceLevel` property from:
   ```
   Info
   ```
   to:
   ```
   Verbose
   ```
3. Save the file and close it.

#### Restart Power BI Report Builder
Close and reopen Power BI Report Builder to apply the changes.

#### Locate the Log Files
The log files are stored in the `Traces` folder at:
```
%LocalAppData%\Microsoft\Power BI Report Builder\15.7\Traces
```
The log file name is `PowerBIReportBuilder.log`.

### BTW, for Microsoft Report Builder (On-prem SSRS or PBIRS)
The configuration file and `Traces` folder are located at:
```
%LocalAppData%\Microsoft\Microsoft Report Builder\
```
