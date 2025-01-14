<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

## Introduction

In this post, we'll discuss how to ensure that the dataset refreshed time in Power BI is always displayed in UTC+8, regardless of whether you're viewing it in Power BI Desktop or Power BI Service. This solution addresses the issue where the time is shown correctly in Power BI Desktop but appears as UTC time in Power BI Service.

## The Problem

When working with Power BI, you might want to display the dataset's refreshed time in a specific time zone (UTC+8 in this case). However, you may encounter an issue where the time is displayed correctly in Power BI Desktop (which uses your local system time) but shows as UTC time when the report is published to Power BI Service.

## The Solution

To solve this problem, we use an M query that adjusts the time zone to UTC+8. Here's the M query that accomplishes this:

```m
let
    Source = DateTimeZone.UtcNow(),
    #"Converted to Table" = #table(1, {{Source}}),
    #"Changed Type" = Table.TransformColumnTypes(#"Converted to Table",{{"Column1", type datetimezone}}),
    #"Adjusted Time Zone" = Table.TransformColumns(#"Changed Type", {{"Column1", each DateTimeZone.SwitchZone(_, 8), type datetimezone}}),
    #"Renamed Columns" = Table.RenameColumns(#"Adjusted Time Zone",{{"Column1", "Last Refreshed Date/Time"}})
in
    #"Renamed Columns"
```

### Explanation

1. **Get Current UTC Time**: `DateTimeZone.UtcNow()` fetches the current UTC time.
2. **Convert to Table**: The time is converted into a table format.
3. **Set Column Type**: The column type is set to `datetimezone`.
4. **Adjust Time Zone**: The time zone is adjusted to UTC+8 using `DateTimeZone.SwitchZone(_, 8)`. https://learn.microsoft.com/en-us/powerquery-m/datetimezone-switchzone
5. **Rename Column**: The column is renamed to "Last Refreshed Date/Time".

This query ensures that the time is consistently displayed in UTC+8, both in Power BI Desktop and Power BI Service.

## Conclusion

By using the `DateTimeZone.SwitchZone` function in your M query, you can ensure that the dataset refreshed time is always displayed in the desired time zone (UTC+8), regardless of where the report is viewed. This solution helps maintain consistency across different environments.

---

*This blog post was generated with the assistance of AI.*
