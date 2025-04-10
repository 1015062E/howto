
-----------------------------------
To have a successful SSL Certificate binding to Reporting Services, it must have the 4 following properties:

1. The certificate has to have a valid expiration date
2. The certificate has to have a Private Key
3. The certificate has to be Trusted
4. The certificate need to be created for Server Authentication


Often times, people fail to check these things before trying to bind their certificates to Reporting Services, and it would fail. The above is 1 of the 2 reasons it would fail. The second reason would be because your Report Server is not clean of it’s URL or SSLCert reservations.

Perform the below steps before binding your SSL Certificate again, and if it fails to bind again, check with your Security Administrator on the certificate properties needed for Reporting Services.

You can also use the below steps if you are having trouble setting up HTTP URLs for Reporting Services, minus the portion about SSL Certificates.

How to clean the system of Reporting Services URLs, and rebind the URLs

1. Go into Reporting Services Configuration Manager, and first remove all the URLs from the Report Manager/Web Portal URL tab:
![image](https://github.com/user-attachments/assets/fb92e0fd-a69f-4495-bb6b-1248a8b5601d)


2. Now do the same for the Web Service URL tab
   ![image](https://github.com/user-attachments/assets/2306f1e9-391b-47d8-800f-5092419e689c)


4. After clearing this portion, you’ll want to check your URL reservation on the server.
<br>a. Open an Admin Command Prompt
<br>b. Run “netsh http show urlacl”. Better yet, you might want to export the results out into notepad so you can view them; `netsh http show urlacl >> C:\urlac.txt`
<br>c. Find all URLs that have “Reports” or “ReportServer” appended to it. If this is the only instance of Reporting Services on the server, removing the URL binding from Reporting Services Configuration Manager should have also removed all of the URL reservations, but sometimes this does leave some URLs that could not be removed by Reporting Services<br>![image](https://github.com/user-attachments/assets/0abf2dc9-c6e5-4180-91cb-f71b46c0eb8d)



<br>d. If you find any URLs related to Reporting Services, we’ll want to delete those URLs.
<br>e. Run the following command: `netsh http delete urlacl url="YOUR URL HERE"`
<br>i. Example: `netsh http delete urlacl url="http://+:80/Reports/"`


4. Once the URL reservations has been clean, we’ll want to clean the SSL reservations. Please see the following blog:
<br>b. Basically, we’ll need to delete the binding that corresponds to your Certificate Hash, whether it’s the old one or the new one, or both, and then start from scratch. Please look in the properties of the certificate being used to compare. You can access the certificate on the server using mmc.exe, and using the certificate snap-in.
<br>c. Command to show SSL binding: `netsh http show sslcert`
<br>d. Example command to delete:
```cmd
netsh http delete sslcert ipport=[::]:443

netsh http delete sslcert ipport=0.0.0.0:443
```

6. Next, we’ll need to check the rsreportserver.config file. https://learn.microsoft.com/en-us/sql/reporting-services/report-server/rsreportserver-config-configuration-file?view=sql-server-ver16
<br>a. Make a copy of this file so that you have a backup.
<br>b. Find the URLReservations portion. There should be one for the ReportServerWebService and ReportManager. If anything is left inside of the second <URL> blocks, you’ll want to clear it. Only delete the highlighted portion.<br>![image](https://github.com/user-attachments/assets/eac91679-2f97-46c2-9019-700f58137f69)


<br>By default, and without any URLs reserved, it should look like this:<br>![image](https://github.com/user-attachments/assets/4d9a583a-acbb-4ef8-aa86-3ac827f1e347)

<br>c. Scroll to the bottom of the rsreportserver.config file. If there are bindings, they would be located at the very bottom:<br>![image](https://github.com/user-attachments/assets/0fbc7b98-7e0f-47a9-91e0-4a02be470f48)
<br>Clear those out and it should look like this:<br>![image](https://github.com/user-attachments/assets/05bb3560-ccf1-4ebd-99e1-44f72a317dd8)


6. Save the rsreportserver.config file.
7. Now Stop and Start Reporting Services.
8. At this point, everything should be clean, so you can now try to bind the URLs again. Start with the Web Service, and then move to the Web Portal URL.


If you have followed those steps from beginning to end, you should have a clean installation of Reporting Services to work with. If your certificate is failing to bind after this, you have an issue with your certificate. I hope this helps!

-----------------------------------
