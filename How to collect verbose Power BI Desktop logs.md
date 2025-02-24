<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>


1. Terminate all running Power BI Desktop processes on your computer.

2. Clear the folder that contains the Desktop traces. 
   - For Power BI Desktop installed with [PBIDesktopSetup_x64.exe](https://aka.ms/pbiSingleInstaller) file, navigate to:
     ```
     %LOCALAPPDATA%\Microsoft\Power BI Desktop\Traces
     ```
   - For Power BI Desktop installed from [Microsoft Store](ms-windows-store:), navigate to:
     ```
     %USERPROFILE%\Microsoft\Power BI Desktop Store App\Traces
     ```

3. Set the system environment variable `PBI_forceTracing = 1`
   <br>      ![image](https://github.com/1015062E/howto/assets/160798406/c35f758b-f877-4b06-90f9-cff778eb16c8)
   <br><br>Alternatively, you can set this variable by running the following command in the command prompt (make sure to run as administrator):
   ```cmd
   SETX PBI_forceTracing "1" /M
   ```
   <br>      ![image](https://github.com/1015062E/howto/assets/160798406/27c60b97-44f2-4279-9a4b-e49df7b29eed)


<br>![image](https://github.com/user-attachments/assets/bfec31a0-e5cf-41a8-ab04-bad76b3aa78d)<br>

4. Reproduce the issue (the shorter, the better).
   - If the issue is with Data(Table/Query) refresh issue, just click on **Refresh** button in the menu bar.
   - If the issue involves a visual, refresh the visual using the Performance Analyzer.
   - Try to minimize the number of visuals on the page to make the trace shorter.

5. **Close Power BI Desktop**. (Important! This ensures logs could be refreshed to disk from Memory)
Open the log files folder after issue is resproduced, then exit Power BI Destkop app(close all PBI Desktop windows!), compress the entire log files folder(select all files, right click then "send to" -> "Compressed").

**Note:** Please remove these settings after usage to avoid slowing down Power BI Desktop performance during daily use.

If you are asked to upload the captured traces, compress the entire log files folder(as well as the "collect diagnostic information" folder, the path you noted down!) and upload the compressed files to the provided workspace. 
