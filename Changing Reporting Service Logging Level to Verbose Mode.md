Follow the steps below to change the logging level to verbose mode:

1. **Backup the Original File**
   Before making any changes, it's crucial to take a backup of the original `ReportingServicesService.exe.config` file. This ensures that you can revert to the original settings if needed.

2. **Update the Configuration File**
   Open the `ReportingServicesService.exe.config` file in a text editor and locate the following sections:

   ```xml
   <system.diagnostics>
       <switches>
           <add name="DefaultTraceSwitch" value="4" />
       </switches>
   </system.diagnostics>
   <RStrace>
       <add name="FileName" value="ReportServerService_" />
       <add name="FileSizeLimitMb" value="42" />
       <add name="KeepFilesForDays" value="14" />
       <add name="Prefix" value="appdomain, tid, time" />
       <add name="TraceListeners" value="file" />
       <add name="TraceFileMode" value="unique" />
       <add name="Components" value="all:4" />
   </RStrace>
   ```

   Change the `value` of the `DefaultTraceSwitch` and `Components` to `4`. This sets the logging level to verbose mode.

3. **Restart the Service**
   After saving your changes, restart the service for the changes to take effect.

Please note that changing the logging level to verbose mode will generate more detailed logs, which can be helpful for troubleshooting. However, it may also consume more disk space.
