Follow the steps below to change the Reporting Services logging level to verbose mode:

1. **Backup the Original File**
   Before making any changes, it's crucial to take a backup of the original `ReportingServicesService.exe.config` file. This ensures that you can revert to the original settings if needed.

   | RS Version/Env | Default path of the config file(Note: Your Reporting Services might be installed to custom specified folder!!!) |
   | ------ | ------ |
   | SSRS 2016 or earlier | C:\Program Files\Microsoft SQL Server\\**MSRS<Version#>.\<InstanceName>**\Reporting Services\ReportServer\bin\ReportingServicesService.exe.config |
   | SSRS 2017 or later | C:\Program Files\Microsoft SQL Server Reporting Services\SSRS\ReportServer\bin\ReportingServicesService.exe.config |
   | On-Prem Power BI Report Server | C:\Program Files\Microsoft Power BI Report Server\PBIRS\ReportServer\bin\ReportingServicesService.exe.config |

2. **Update the Configuration File**
   Open the `ReportingServicesService.exe.config` file in a text editor and locate the following sections: <br>![image](https://github.com/1015062E/howto/assets/160798406/84337576-6700-461e-ac96-6b589025f382)

   Change the `value` of the `DefaultTraceSwitch` and `Components` to `4`. This sets the logging level to verbose mode.

3. **Restart the Service**
   After saving your changes, restart the service for the changes to take effect.

Please note that changing the logging level to verbose mode will generate more detailed logs, which can be helpful for troubleshooting. However, it may also consume more disk space. So, please dont forget to change the logging level back to INFO (3) after the troubleshooting is done and your issue is fixed. 
