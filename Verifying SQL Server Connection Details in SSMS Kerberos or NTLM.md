<br>
<table>
  <td>WARNING</td>
  <td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

**Disclaimer**: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

## Verifying SQL Server Connection Details in SSMS Kerberos or NTLM

SQL Server Management Studio (SSMS) is a powerful tool for managing SQL Server instances, and understanding connection details such as authentication type (Kerberos or NTLM), application name, and login time is critical for troubleshooting and security auditing. This blog post outlines how to verify these details using Transact-SQL (T-SQL) queries, focusing on a comprehensive query to retrieve connection information. The content is based on a discussion about retrieving authentication types, executable process names, and login times, reorganized for clarity and logical flow.

### Why Verify Connection Details?

Verifying connection details helps database administrators:
- Confirm whether connections use secure authentication methods like Kerberos.
- Identify the applications (e.g., SSMS) connecting to the server.
- Monitor login and connection times for auditing or performance analysis.
- Diagnose issues such as unexpected NTLM authentication or connection failures.

This post provides a single, consolidated T-SQL query to retrieve these details and explains how to interpret the results.

### Prerequisites

To follow the steps in this post, ensure you have:
- Access to SSMS connected to a SQL Server instance.
- `VIEW SERVER STATE` permission to query dynamic management views (DMVs).
- Basic familiarity with T-SQL and SQL Server authentication concepts.

### Consolidated T-SQL Query for Connection Details

The following T-SQL query retrieves key connection details, including authentication type, login time, application name, and more, for all user sessions or the current session:

```sql
SELECT 
    c.session_id AS SessionID,
    c.auth_scheme AS AuthenticationType,
    s.login_time AS LoginTime,
    c.connect_time AS ConnectTime,
    s.program_name AS ProgramName,
    s.host_name AS HostName,
    s.login_name AS LoginName,
    s.client_interface_name AS ClientInterface,
    c.protocol_type AS ProtocolType,
    c.net_transport AS NetTransport,
    s.status AS SessionStatus
FROM 
    sys.dm_exec_connections c
INNER JOIN 
    sys.dm_exec_sessions s
ON 
    c.session_id = s.session_id
WHERE 
    s.is_user_process = 1
    -- Optionally filter for current session: AND c.session_id = @@SPID
ORDER BY 
    s.program_name DESC, s.login_time DESC;
```

#### Query Breakdown
- **Columns Retrieved**:
  - `SessionID`: Unique identifier for the session.
  - `AuthenticationType`: Authentication method ("KERBEROS", "NTLM", or "SQL").
  - `LoginTime`: Timestamp when the session was authenticated.
  - `ConnectTime`: Timestamp when the connection was established.
  - `ProgramName`: Application name (e.g., "Microsoft SQL Server Management Studio").
  - `HostName`: Client machine name (e.g., "CLIENT-PC").
  - `LoginName`: SQL Server or Windows login (e.g., "domain\user").
  - `ClientInterface`: Client interface (e.g., ".Net SqlClient Data Provider").
  - `ProtocolType`: Protocol used (e.g., "TSQL").
  - `NetTransport`: Network transport (e.g., "TCP", "Shared Memory").
  - `SessionStatus`: Session status (e.g., "running", "sleeping").
- **Filters and Joins**:
  - `INNER JOIN` links `sys.dm_exec_connections` and `sys.dm_exec_sessions` on `session_id`.
  - `is_user_process = 1` excludes system processes.
  - The optional `AND c.session_id = @@SPID` filters for the current session (uncomment to use).
- **Sorting**: Results are sorted by `program_name` (descending) and `login_time` (descending) for organized output.

#### Example Output
Executing the query might yield:
```
SessionID | AuthenticationType | LoginTime            | ConnectTime          | ProgramName                          | HostName   | LoginName     | ClientInterface                | ProtocolType | NetTransport | SessionStatus
----------|--------------------|----------------------|----------------------|--------------------------------------|------------|---------------|--------------------------------|--------------|--------------|---------------
51        | KERBEROS           | 2025-05-26 10:00:05 | 2025-05-26 10:00:00 | Microsoft SQL Server Management Studio | CLIENT-PC | domain\user   | .Net SqlClient Data Provider | TSQL         | TCP          | running
52        | NTLM               | 2025-05-26 09:55:10 | 2025-05-26 09:55:05 | Microsoft SQL Server Management Studio | SERVER-PC | domain\admin  | .Net SqlClient Data Provider | TSQL         | Shared Memory| sleeping
53        | SQL                | 2025-05-26 09:50:00 | 2025-05-26 09:50:00 | CustomApp                            | APP-PC    | sqluser       | ODBC Driver                  | TSQL         | TCP          | running
```

### Interpreting the Results

- **Authentication Type**:
  - "KERBEROS" indicates a secure, ticket-based authentication.
  - "NTLM" suggests a less secure fallback, often due to missing Service Principal Names (SPNs) or local connections.
  - "SQL" indicates SQL Server authentication.
- **Program Name**: For SSMS, expect "Microsoft SQL Server Management Studio". To confirm the exact executable (e.g., `ssms.exe`), use Windows Task Manager on the client machine.
- **Login and Connect Times**: These timestamps help track session duration and identify long-running connections.
- **Net Transport**: "Shared Memory" for local connections, "TCP" for remote connections.

### Troubleshooting Common Issues

If the query shows unexpected results:
- **NTLM Instead of Kerberos**:
  - Verify SPNs using `setspn -L domain\service_account`.
  - Ensure time synchronization between client, server, and domain controller (within 5 minutes).
  - Note that local connections always use NTLM due to Windows security hardening.
- **Permission Errors**: Ensure the login has `VIEW SERVER STATE` permission.
- **Missing Details**: Use Windows Event Viewer (Event ID 4624) or Microsoft Kerberos Configuration Manager for deeper diagnostics.

### Additional Verification Methods

Beyond the T-SQL query, you can:
- **Use SSMS Activity Monitor**: Right-click the server in SSMS, select "Activity Monitor", and review the "Processes" section for connection details.
- **Check SQL Server Error Logs**: Navigate to "Management" > "SQL Server Logs" or use `xp_readerrorlog` to find authentication details.
- **Run `klist`**: On the client, use `klist` in Command Prompt to verify Kerberos tickets for the SQL Server’s SPN (e.g., `MSSQLSvc/SQLServerFQDN:1433`).

### Best Practices

- Run SQL Server services under a domain account with minimal permissions to support Kerberos.
- Use tools like Microsoft Kerberos Configuration Manager to validate SPNs.
- Ensure TCP/IP is enabled in SQL Server Configuration Manager for remote Kerberos connections.
- Regularly audit connections for security and performance.
