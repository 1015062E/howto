<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>


Change supported authentication types for the Reporting Services(or Report Server) to below.

[Configure Windows authentication on the report server](https://learn.microsoft.com/en-us/sql/reporting-services/security/configure-windows-authentication-on-the-report-server?view=sql-server-ver16)

```
<AuthenticationTypes>
    <RSWindowsNegotiate/>
    <RSWindowsNTLM/>
</AuthenticationTypes>
```

Then : 
<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/ee29f824-81a3-4e98-b5d2-0cc8d2589392)

<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/02db7f96-8001-40ce-8e38-8be54f553857)

<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/53ad7501-4667-497c-97db-ce52bfc3c080)

<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/1a41c6dd-bbd4-4d2a-babe-5108f1bb6841)
