<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

## Understanding "Enable Load" and "Include in Report Refresh" Options in Power BI Desktop

### Introduction
In Power BI Desktop, managing data efficiently is crucial for performance and usability. Two important options that help in this regard are "Enable Load" and "Include in Report Refresh." This blog post will explain these options, their interactions, and practical use cases.

### Enable Load
The "Enable Load" option determines whether a table's data is loaded into the data model. When disabled, the table's data is not available for use in report visuals, calculations, or relationships.

#### Example 1: Intermediate Transformation
1. **Table 1**: Load sales transactions data (Enable Load: **Yes**).
2. **Table 2**: Categorize transactions from Table 1 (Enable Load: **No**).
3. **Table 3**: Merge Table 2 with another dataset (Enable Load: **Yes**).

In this example, Table 1 must have "Enable Load" enabled because Table 2 depends on its data. Table 2 can have "Enable Load" disabled as it's an intermediate step, and Table 3 will be the final table loaded into the data model.

### Include in Report Refresh
The "Include in Report Refresh" option controls whether a table is refreshed when you refresh your report. This is useful for tables with static or rarely changing data.

#### Example 2: Data Preparation
1. **Table 1**: Load January sales data (Enable Load: **No**, Include in Report Refresh: **No**).
2. **Table 2**: Load February sales data (Enable Load: **No**, Include in Report Refresh: **No**).
3. **Table 3**: Append Table 1 and Table 2 to create a combined dataset (Enable Load: **Yes**, Include in Report Refresh: **Yes**).

In this scenario, Table 1 and Table 2 are intermediate steps and do not need to be loaded into the data model. Only Table 3, the final combined dataset, is loaded and refreshed.

### Interaction Between Options
When "Enable Load" is unchecked, "Include in Report Refresh" is automatically disabled. This is because if a table is not loaded into the data model, refreshing it is unnecessary.

### Practical Implications
- **Intermediate Tables**: Disable "Enable Load" to save memory and improve performance. These tables won't be refreshed as part of the report refresh.
- **Final Tables**: Keep "Enable Load" enabled and ensure "Include in Report Refresh" is also enabled to keep the data up-to-date.

### Conclusion
Understanding how to use "Enable Load" and "Include in Report Refresh" options effectively can significantly enhance your Power BI reports' performance and manageability. Use these options to control which tables are loaded and refreshed, optimizing your data model for better performance.

---
<br>https://learn.microsoft.com/en-us/power-bi/connect-data/refresh-include-in-report-refresh
