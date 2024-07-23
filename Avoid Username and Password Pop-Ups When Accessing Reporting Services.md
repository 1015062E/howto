1. Change supported authentication types for the Reporting Services(or Report Server) to below.
- Please follow [Reporting Services/Reporting Services Installation Path.md](https://github.com/guoqingsun-msft/guoqingsun/blob/main/Reporting%20Services/Reporting%20Services%20Installation%20Path.md) to determine where the configuraiton file RsReportServer.config is. 
- Update the config file RsReportServer.config for all instances in a scale-out group (Skip if your SSRS/PBIRS is a standalone instance)
- (Case Sensitive, Order matters!)
```
<AuthenticationTypes>
    <RSWindowsNegotiate/>
    <RSWindowsNTLM/>
</AuthenticationTypes>
```

2. Then follow - 
<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/ee29f824-81a3-4e98-b5d2-0cc8d2589392)

<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/02db7f96-8001-40ce-8e38-8be54f553857)

<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/53ad7501-4667-497c-97db-ce52bfc3c080)

<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/1a41c6dd-bbd4-4d2a-babe-5108f1bb6841)
