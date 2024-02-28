1. Terminate all running Power BI Desktop processes on your computer.

2. Clear the folder that contains the Desktop traces. 
   - For Power BI Desktop MSI, navigate to: `%LOCALAPPDATA%\Microsoft\Power BI Desktop\Traces` 
     <br>![image](https://github.com/1015062E/howto/assets/160798406/a44e79b0-23b3-4359-8b00-f99ad9371925)
   - For Power BI Desktop from the Store, navigate to: `%USERPROFILE%\Microsoft\Power BI Desktop Store App\Traces`

3. Set the system environment variable `PBI_forceTracing = 1`
   <br>      ![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/5420630f-1638-4dfe-b083-7f397fd946b7)
   <br><br>Alternatively, you can set this variable by running the following command in the command prompt (make sure to run as administrator):
   ```cmd
   SETX PBI_forceTracing "1" /M
   ```
   <br>      ![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/2c84f0ed-1e25-4314-aa04-e10c9e1b8f34)

4. Reproduce the issue (the shorter, the better).
   - If the issue involves a visual, refresh the visual using the Performance Analyzer.
   - Try to minimize the number of visuals on the page to make the trace shorter.

5. Close Power BI Desktop.

6. Review the files present (one PBIDesktop log, one msmdsrv log, one TRC file and zero or several Mashup traces).

**Note:** Please remove these settings after usage to avoid slowing down Power BI Desktop performance during daily use.

If you are asked to upload the captured traces, compress the entire folder and upload the compressed file to the provided workspace. 
<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/ac6b64c1-8200-484b-9cb5-eb96dc9c525e)
