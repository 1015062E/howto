Install Fiddler from https://telerik-fiddler.s3.amazonaws.com/fiddler/FiddlerSetup.exe if it doesnt exist in the computer. 
1. (1) If the issue occurs in Internet Browser, close all other browsers windows/tabs and keep only the tab we want to focus on.  (2) If the issue is with other client app (e.g. Power BI Desktop, Excel, SSMS, on-prem Gateway etc.) please ensure there's only one window of it is running.
2. Launch fiddler(**Run as Administrator**), then click Tools >  Options
3. Click the ‘HTTPS’ tab.
4. Verify the options are set as shown in this screenshot. (Confirm that the Decrypt HTTPS traffic is checked)<br>![image](https://github.com/1015062E/howto/assets/160798406/fe635c5e-b8ea-43f0-8bd6-465b9b899725)

	 
5. If fiddler prompts you to trust their root certificates, then click ‘Yes’, OK, Next etc.
6. Exit Fiddler app then Start it again with **Run as Administrator**;
7. Then reproduce the problem when fiddler is capturing traffic at the backend. <br>![image](https://github.com/1015062E/howto/assets/160798406/35c7e0aa-a929-4710-909a-856ee50cbe90)

8. After the trace is captured, go to File > uncheck box next to Capture Traffic (or just press F12)
9. Click File > Save > All Sessions
10. COMPRESS (compress it to a .zip) send upload the comporessed file to the secure FTP workspace shared with you. 
	 
Note: Please feel free to **uninstall** this application from your computer after collecting the trace(Or after the issue got resolved finally)
