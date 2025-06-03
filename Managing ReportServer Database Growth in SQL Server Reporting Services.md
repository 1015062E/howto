<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

## Managing ReportServer Database Growth in SQL Server Reporting Services

Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

### Introduction

The `ReportServer` database in SQL Server Reporting Services (SSRS) can grow significantly over time, especially in large-scale environments. This blog post discusses a real-world scenario where the `ReportServer` database grew to over 2 TB, identifies the root causes, and provides actionable recommendations to manage and reduce database size effectively.

### Problem Analysis

The primary issue was the rapid growth of the `ReportServer` database, with the largest table being the `Segment` table. Below is a summary of the table sizes:

| Table Name            | Rows       |
|-----------------------|------------|
| Segment               | 246,047,355 |
| ChunkSegmentMapping   | 142,034,246 |
| SegmentedChunk        | 494,531     |
| SnapshotData          | 74,891      |

#### Key Findings
1. **Snapshots**:
   - Snapshots were not actively used, but 60k rows in the `SnapshotData` table were linked to the `History` table, indicating past usage.
   - Snapshots do not expire automatically and require manual cleanup.

2. **Intermediate Format**:
   - Reports deployed to SSRS are converted to an intermediate format and stored in the database. Larger RDL files result in more rows in the `Segment`, `SegmentedChunk`, and `ChunkSegmentMapping` tables.

3. **Orphaned Rows**:
   - Approximately 40% of rows in the `Segment` table were orphaned and could be removed.

4. **Cleanup Process**:
   - The default cleanup process runs daily at 2 AM but does not target orphaned rows in these tables.
   - Stored procedures `RemoveSegment` and `RemoveSegmentedMapping` are limited to deleting 100 and 1,000 rows per run, respectively, which is insufficient for large-scale environments.

5. **Concurrency Issues**:
   - In a scale-out deployment with multiple servers, all servers run the cleanup process simultaneously, causing contention and inefficiencies.

### Recommendations

#### **1. Manual Cleanup**
Run the stored procedures `RemoveSegment` and `RemoveSegmentedMapping` manually with larger parameter values to expedite cleanup. Example:
```sql
EXEC RemoveSegment @MaxRows = 10000;
EXEC RemoveSegmentedMapping @MaxRows = 10000;
```

#### **2. Automate Cleanup with SQL Agent Jobs**
Set up a SQL Agent job to run the cleanup procedures during off-hours with higher parameter values. Example:
```sql
-- SQL Agent Job Script
EXEC RemoveSegment @MaxRows = 5000;
EXEC RemoveSegmentedMapping @MaxRows = 5000;
```

#### **3. Stagger Cleanup Times**
Modify the `rsreportserver.config` file to stagger the cleanup times across servers in a scale-out deployment. Example:
```xml
<DailyCleanupMinute>120</DailyCleanupMinute> <!-- 2:00 AM -->
<DailyCleanupMinute>180</DailyCleanupMinute> <!-- 3:00 AM -->
```

#### **4. Identify Orphaned Records**
Use the following SQL queries to identify orphaned records in key tables:

- **Orphaned Rows in `SegmentedChunk`**:
  ```sql
  SELECT * 
  FROM SegmentedChunk 
  WHERE SnapshotDataId NOT IN (SELECT SnapshotDataID FROM SnapshotData);
  ```

- **Orphaned Rows in `SnapshotData`**:
  ```sql
  SELECT COUNT(*) 
  FROM SnapshotData 
  WHERE SnapshotDataID NOT IN (
      SELECT Intermediate FROM Catalog WHERE Intermediate IS NOT NULL
      UNION
      SELECT SnapshotDataID FROM Catalog WHERE SnapshotDataID IS NOT NULL
      UNION
      SELECT SnapshotDataID FROM History
  ) 
  AND PaginationMode IS NOT NULL 
  AND PermanentRefcount > 0;
  ```

#### **5. Mark Records for Cleanup**
Mark orphaned records in the `SnapshotData` table for cleanup:
```sql
UPDATE SnapshotData 
SET PermanentRefcount = 0 
WHERE SnapshotDataID NOT IN (
    SELECT Intermediate FROM Catalog WHERE Intermediate IS NOT NULL
    UNION
    SELECT SnapshotDataID FROM Catalog WHERE SnapshotDataID IS NOT NULL
    UNION
    SELECT SnapshotDataID FROM History
) 
AND PaginationMode IS NOT NULL 
AND PermanentRefcount > 0;
```

#### **6. Optimize Cleanup Parameters**
Increase the default cleanup batch size by modifying stored procedures. For example, replace `DELETE TOP(20)` with a higher value:
```sql
DELETE TOP(100) -- Adjust the value as needed
```

### SQL Queries for Monitoring and Analysis

#### **Get Row Count of Each Table**
```sql
SELECT OBJ.Name AS TABLES, 
       IDX.Rows AS ROWS_COUNT 
FROM sys.sysobjects AS OBJ 
INNER JOIN sys.sysindexes AS IDX 
    ON OBJ.id = IDX.id 
WHERE type = 'U' 
  AND IDX.IndId < 2 
ORDER BY IDX.Rows DESC;
```

#### **Identify Rows for Cleanup**
```sql
SELECT COUNT(*) AS Segment 
FROM Segment WITH (READPAST) 
WHERE NOT EXISTS (
    SELECT 1 
    FROM ChunkSegmentMapping CSM WITH (NOLOCK) 
    WHERE CSM.SegmentId = Segment.SegmentId
);
```

### Conclusion

Managing the growth of the `ReportServer` database requires a combination of manual and automated cleanup processes, configuration changes, and monitoring. By implementing the recommendations outlined in this post, you can effectively reduce database size and improve the performance of your SSRS environment.
