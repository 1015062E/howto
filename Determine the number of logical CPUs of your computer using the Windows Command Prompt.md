Type the following command and press Enter in cmd Windows Command Prompt:

```cmd
wmic cpu get NumberOfLogicalProcessors
```
![image](https://github.com/1015062E/howto/assets/160798406/dfe2caa1-4d2b-4434-829e-e5d7da1fbaee)

This command uses the Windows Management Instrumentation Command-line (WMIC) to retrieve the number of logical processors. The output will display the number of logical CPUs for each physical CPU in your system. If you have a single CPU, it will display the number of logical CPUs for that CPU.

Remember, the number of logical processors is typically twice the number of cores if hyper-threading is enabled on the system. If hyper-threading is disabled, the number of logical processors will be equal to the number of cores. 

Please note that you might need administrative privileges to run this command. If you encounter any issues, try running the Command Prompt as an administrator. To do this, right-click on the Command Prompt in the Start menu and select `Run as administrator`. Then, enter the command as before.<br>

--------------------------------------------
<br>You can also use the Task Manager to check the number of logical processors on your computer. Here's how:
1. Press `Ctrl + Shift + Esc` to open the Task Manager.
2. If it opens in the simplified view, click on `More details` at the bottom.
3. Go to the `Performance` tab.
4. Click on `CPU` in the left pane.

In the bottom right corner, you'll see information about your CPU, including the number of cores and logical processors. The number of logical processors is typically twice the number of cores if hyper-threading is enabled on the system. If hyper-threading is disabled, the number of logical processors will be equal to the number of cores. 
![image](https://github.com/1015062E/howto/assets/160798406/f130feef-c38c-49f5-9662-7af84afc8332)
