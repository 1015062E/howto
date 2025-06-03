<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

## Retrieve a list of users their roles and the paths of items they have access to in the Reporting Services

### Overview

This blog post provides an analysis of a SQL Server query designed to retrieve user, role, and item path information from the `ReportServer` database of SQL Server Reporting Services (SSRS). The query is useful for auditing or managing permissions within the Reporting Services environment.

### The Query

```sql
SELECT 
    u.UserName,
    r.RoleName,
    c.Path
FROM 
    dbo.PolicyUserRole pur
JOIN 
    dbo.Users u ON pur.UserID = u.UserID
JOIN 
    dbo.Roles r ON pur.RoleID = r.RoleID
JOIN 
    dbo.Catalog c ON pur.PolicyID = c.PolicyID
--WHERE 
--    c.Path LIKE '/YourFolderPath%'
```

### Explanation of the Query

#### Selected Columns
- **`u.UserName`**: Retrieves the username of the user.
- **`r.RoleName`**: Retrieves the name of the role assigned to the user.
- **`c.Path`**: Retrieves the path of the item (e.g., folder, report, or resource) in the Reporting Services catalog.

#### Tables and Joins
The query uses the following tables from the `ReportServer` database:
1. **`dbo.PolicyUserRole` (`pur`)**:
   - Links users, roles, and policies in Reporting Services.
2. **`dbo.Users` (`u`)**:
   - Contains user information, such as `UserID` and `UserName`.
3. **`dbo.Roles` (`r`)**:
   - Contains role information, such as `RoleID` and `RoleName`.
4. **`dbo.Catalog` (`c`)**:
   - Represents the catalog of items in Reporting Services, including reports, folders, and resources. It also includes the `Path` and `PolicyID` of each item.

The query joins these tables to link users, roles, and catalog items:
- `pur.UserID = u.UserID`: Links the `PolicyUserRole` table to the `Users` table.
- `pur.RoleID = r.RoleID`: Links the `PolicyUserRole` table to the `Roles` table.
- `pur.PolicyID = c.PolicyID`: Links the `PolicyUserRole` table to the `Catalog` table.

#### Optional Filtering
The commented-out `WHERE` clause:
```sql
--WHERE 
--    c.Path LIKE '/YourFolderPath%'
```
If uncommented, this would filter the results to include only items whose paths start with `/YourFolderPath`.

### Use Case

This query is particularly useful for:
- **Auditing**: Identifying which users have access to specific items in the Reporting Services catalog.
- **Permission Management**: Reviewing and managing user roles and their associated permissions.

### Important Notes

- **Sensitive Information**: Ensure that sensitive or personally identifiable information (PII) is handled appropriately when running or sharing the results of this query.
- **Customization**: Modify the `WHERE` clause to target specific folders or paths as needed for your use case.

### Conclusion

This query provides a straightforward way to retrieve user, role, and item path information from the `ReportServer` database in SQL Server Reporting Services. It is a valuable tool for administrators managing permissions and auditing access within the SSRS environment.

For further customization or assistance, consult the official SQL Server Reporting Services documentation or your database administrator.
