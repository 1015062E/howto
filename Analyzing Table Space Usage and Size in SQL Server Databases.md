<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

## Analyzing Table Space Usage in SQL Server Databases

### Introduction
Managing space effectively in a SQL Server database is crucial for optimizing performance and maintaining system health. The query discussed in this post provides insights into space usage by user-created tables, including details about allocated, used, and unused space. This analysis can be used to identify large tables, understand storage patterns, and support maintenance tasks.

### The Query Explained
The SQL query retrieves detailed information about space usage for all user tables in a database. 
```sql
SELECT 
    t.NAME AS TableName,
    s.Name AS SchemaName,
    p.rows,
    SUM(a.total_pages) * 8 AS TotalSpaceKB, 
    CAST(ROUND(((SUM(a.total_pages) * 8) / 1024.00), 2) AS NUMERIC(36, 2)) AS TotalSpaceMB,
    SUM(a.used_pages) * 8 AS UsedSpaceKB, 
    CAST(ROUND(((SUM(a.used_pages) * 8) / 1024.00), 2) AS NUMERIC(36, 2)) AS UsedSpaceMB, 
    (SUM(a.total_pages) - SUM(a.used_pages)) * 8 AS UnusedSpaceKB,
    CAST(ROUND(((SUM(a.total_pages) - SUM(a.used_pages)) * 8) / 1024.00, 2) AS NUMERIC(36, 2)) AS UnusedSpaceMB
FROM 
    sys.tables t
INNER JOIN      
    sys.indexes i ON t.OBJECT_ID = i.object_id
INNER JOIN 
    sys.partitions p ON i.object_id = p.OBJECT_ID AND i.index_id = p.index_id
INNER JOIN 
    sys.allocation_units a ON p.partition_id = a.container_id
LEFT OUTER JOIN 
    sys.schemas s ON t.schema_id = s.schema_id
WHERE 
    t.NAME NOT LIKE 'dt%' 
    AND t.is_ms_shipped = 0
    AND i.OBJECT_ID > 255 
GROUP BY 
    t.Name, s.Name, p.Rows
ORDER BY 
    TotalSpaceMB DESC, t.Name
```

<br><img width="745" alt="image" src="https://github.com/user-attachments/assets/9a7f8d46-af29-4d36-bf08-243ec021bbb4" />

Below is a breakdown of its purpose and functionality:

#### Columns Retrieved
1. **Table Name**: Displays the name of each table.
2. **Schema Name**: Indicates the schema to which the table belongs.
3. **Row Count**: Shows the number of rows in the table.
4. **Total Space (KB/MB)**: Total space allocated to the table.
5. **Used Space (KB/MB)**: Space actually used by the table.
6. **Unused Space (KB/MB)**: Free space within the allocated storage.

#### Data Sources and Joins
- **`sys.tables`**: Contains metadata about tables.
- **`sys.indexes`**: Links tables to their storage structures.
- **`sys.partitions`**: Provides partition-level information.
- **`sys.allocation_units`**: Tracks storage allocation details.
- **`sys.schemas`**: Identifies the schema of each table.

#### Key Filters
- Excludes system tables (e.g., names starting with `dt` or Microsoft-shipped tables).
- Ensures only user-created objects are included.

#### Aggregation and Grouping
The query groups tables by name, schema, and row count. It calculates total, used, and unused space by aggregating page-level storage information.

### Practical Use Cases
This query can support:
1. **Performance Optimization**: Identifying large tables consuming excessive space.
2. **Capacity Planning**: Monitoring database growth and planning for storage expansion.
3. **Maintenance Tasks**: Reclaiming unused space or reorganizing fragmented storage.

### Caveats and Considerations
- This query is read-only and safe to execute on production databases.
- It excludes temporary tables and system tables by default.
- Always validate the results and ensure they are relevant to your specific use case.

### Conclusion
The provided query is a powerful tool for analyzing table space usage in SQL Server databases. By understanding how space is allocated and utilized, database administrators can make informed decisions about optimization and storage management. Ensure you test this query in a non-production environment before applying it broadly.

### References
For more information, refer to [Microsoft SQL Server Documentation](https://learn.microsoft.com/en-us/sql/sql-server/).

