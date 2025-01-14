<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>
> _Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case._

## Understanding the Difference Between Two Queries for `$SYSTEM.DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS`

When working with metadata in environments like Microsoft Analysis Services (SSAS) or Azure Analysis Services (AAS), you might encounter different ways to query the `$System.DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS` system view. This blog post explains the differences between two common query patterns:

---

## Query 1: Direct Query with `WHERE`

```sql
SELECT * 
FROM $SYSTEM.DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS
WHERE [DATABASE_NAME] = 'YourModelName'
```

### Key Characteristics:
1. **Direct Query**:
   - Queries the `$SYSTEM.DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS` system view directly.
   
2. **Filter Application**:
   - The `WHERE` clause filters rows where `[DATABASE_NAME]` matches `'YourModelName'`.

3. **Use Case**:
   - Ideal for users with full access to the `$System` views and familiarity with standard SQL syntax.

4. **Behavior**:
   - Returns all rows matching the filter condition.
   - Requires appropriate permissions on the `$System` view.

---

## Query 2: Using `SYSTEMRESTRICTSCHEMA`

```sql
SELECT * FROM SYSTEMRESTRICTSCHEMA ($System.DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS, [DATABASE_NAME] = '<Dataset Name>')
```

### Key Characteristics:
1. **Restricted Schema Query**:
   - Applies a filter directly at the schema level using `SYSTEMRESTRICTSCHEMA`.

2. **Filter Integration**:
   - The filter condition (`[DATABASE_NAME] = '<Dataset Name>'`) is passed as a parameter to the `SYSTEMRESTRICTSCHEMA` function.

3. **Use Case**:
   - Useful in environments with restricted access to system views or when schema-level filtering is preferred.

4. **Behavior**:
   - May be slightly more performant since the filtering is applied during querying.
   - Often suitable for scenarios with limited permissions on the `$System` views.

---

## Key Differences

| Aspect                     | Query 1                                     | Query 2                                         |
|----------------------------|---------------------------------------------|------------------------------------------------|
| **Syntax**                 | Standard SQL with a `WHERE` clause.        | Uses the `SYSTEMRESTRICTSCHEMA` function.      |
| **Filtering**              | Applied after querying the view.           | Applied directly during querying.              |
| **Permissions**            | Requires access to the full `$System` view.| May allow for restricted access.               |
| **Performance**            | Filtering happens post-query.              | Integrated filtering might optimize results.   |
| **Readability**            | Familiar SQL structure.                    | More concise but less familiar.                |

---

## Choosing the Right Query

### Use Query 1:
- When you have unrestricted access to the `$System` views.
- If you need flexibility with query construction.

### Use Query 2:
- When your access is restricted.
- If schema-level filtering is required for performance or security.

---

## Final Notes
Understanding the nuances between these queries can help you choose the right one for your needs. Be mindful of permissions, performance, and the specific requirements of your environment.

**Acknowledgment**: This blog post was generated with AI assistance. Please verify the content for your specific use case to ensure its accuracy.
