1. Terminate all running Power BI Desktop processes on your computer.

2. Clear the folder that contains the Desktop traces. 
   - For Power BI Desktop installed with [PBIDesktopSetup_x64.exe](https://aka.ms/pbiSingleInstaller) file, navigate to: `%LOCALAPPDATA%\Microsoft\Power BI Desktop\Traces` 
     <br>![image](https://github.com/1015062E/howto/assets/160798406/a44e79b0-23b3-4359-8b00-f99ad9371925)
   - For Power BI Desktop from (Microsoft Store)[ms-windows-store://?referrer=storeforweb], navigate to: `%USERPROFILE%\Microsoft\Power BI Desktop Store App\Traces`

3. Set the system environment variable `PBI_forceTracing = 1`
   <br>      ![image](https://github.com/1015062E/howto/assets/160798406/c35f758b-f877-4b06-90f9-cff778eb16c8)
   <br><br>Alternatively, you can set this variable by running the following command in the command prompt (make sure to run as administrator):
   ```cmd
   SETX PBI_forceTracing "1" /M
   ```
   <br>      ![image](https://github.com/1015062E/howto/assets/160798406/27c60b97-44f2-4279-9a4b-e49df7b29eed)


<br>![image](https://github.com/1015062E/howto/assets/160798406/a4b3e144-c3f4-4d15-9a4f-7d01b7f288a5)
<br>

4. Reproduce the issue (the shorter, the better).
   - If the issue involves a visual, refresh the visual using the Performance Analyzer.
   - Try to minimize the number of visuals on the page to make the trace shorter.

5. Close Power BI Desktop.

6. Review the files present (one PBIDesktop log, one msmdsrv log, one TRC file and zero or several Mashup traces).

**Note:** Please remove these settings after usage to avoid slowing down Power BI Desktop performance during daily use.

If you are asked to upload the captured traces, compress the entire folder and upload the compressed file to the provided workspace. 
<br>![image](https://github.com/1015062E/howto/assets/160798406/ca8a600f-8e68-4aa0-9379-86b49eef4b30)
<br> OR : ![image](https://github.com/1015062E/howto/assets/160798406/80c309b6-4200-4321-ac6b-0335c5ced8df)
