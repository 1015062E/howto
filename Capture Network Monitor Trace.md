To capture network traces for troubleshooting, it is recommended to capture the trace from both the client and server computers simultaneously. 

However, if the server is a third-party product (e.g. SaaS/PaaS) and you don't have access (RDP) to the server, you just need to capture the trace from your client computer.  

If the requests from the client could be dispatched to a random server, and you or your team have access/RDP to the servers, you may need to run Network Monitor on all possible servers. Alternatively, you can deactivate some servers to ensure the traffic only routes to one server, which simplifies the troubleshooting process.


## Steps to capture Network traces
1. Please download Network Monitor tool (**NM34_x64.exe** for most users) from https://www.microsoft.com/en-us/download/details.aspx?id=4865, and install it to your client and server(s) computers (right click on the installationf file and select **'Run as admin'**).
2. Click on Windows Start and search **'NetMon'**(or **'Network Monitor'**) then run it AS ADMINISTRATOR (This is required for capturing traces).<br>![image](https://user-images.githubusercontent.com/85205970/233249937-897253ce-f668-4cdc-9964-e7b5394e2062.png)

3. In the **'Select Networks**' pane, choose which adapters to capture. Normally, the defaults are sufficient. (Keeping the default selections is okay) <br>![image](https://user-images.githubusercontent.com/85205970/233250244-bdfcd53f-d5ef-4a29-abc4-832c970eaf1d.png)

4. Click on **'New Capture'** in the toolbar. This will create a new Tab, e.g. Capture 1. <br>![image](https://user-images.githubusercontent.com/85205970/233250299-b3c6c61c-4b54-4e1f-a15a-f39789eba75a.png)

5. Clear DNS/Kerberos cache by running below commands in Command Prompt Window from within Server.
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ipconfig /flushdns<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;klist purge

6. Find **'Start'** and **'Stop'** buttonse. Click on **'Start**' for all the involved computers(client and servers) before reproducing the issue. Click on **'Stop'** button for all NetMon after issue got reproduced.<br>![image](https://user-images.githubusercontent.com/85205970/233250456-a214a900-bf28-4549-98db-795a94218a7d.png)

7. With the Capture tab selected, use **'File'** -> **'Save As'** or **'Save As'** button in the toolbar to save the trace to a .CAP file(Note down the path in case you forgot where it was saved to). <br>![image](https://user-images.githubusercontent.com/85205970/233250616-75e14685-fd60-4633-ab9b-a9d65062410b.png)

9. Collect IP and port information from all related computers by executing commands below in elevated CMD window.
```cmd
ipconfig /all >> C:\%COMPUTERNAME%.%USERDNSDOMAIN%_IPconfig.txt
```
```cmd
netstat -abno >> C:\%COMPUTERNAME%.%USERDNSDOMAIN%_Netstat.txt
```

9. Please Compress and upload above files(Netmon trace, IP info file, Ports info file) to the workspace shared with you. 
(Note : Please do COMPRESS all those files to a single .zip file before uploading, thanks~ )
