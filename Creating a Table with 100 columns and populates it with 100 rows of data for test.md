<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

A SQL script that creates a table with 100 columns and populates it with 100 rows of data.

### Table Creation

```sql
use [0_MIKE_TEST_DB]
CREATE TABLE Table_with_100_columns_n_100_rows (
    ID INT IDENTITY(1,1) PRIMARY KEY,
    Col001 CHAR(1),
    Col002 CHAR(1),
    Col003 CHAR(1),
    Col004 CHAR(1),
    Col005 CHAR(1),
    Col006 CHAR(1),
    Col007 CHAR(1),
    Col008 CHAR(1),
    Col009 CHAR(1),
    Col010 CHAR(1),
    Col011 CHAR(1),
    Col012 CHAR(1),
    Col013 CHAR(1),
    Col014 CHAR(1),
    Col015 CHAR(1),
    Col016 CHAR(1),
    Col017 CHAR(1),
    Col018 CHAR(1),
    Col019 CHAR(1),
    Col020 CHAR(1),
    Col021 CHAR(1),
    Col022 CHAR(1),
    Col023 CHAR(1),
    Col024 CHAR(1),
    Col025 CHAR(1),
    Col026 CHAR(1),
    Col027 CHAR(1),
    Col028 CHAR(1),
    Col029 CHAR(1),
    Col030 CHAR(1),
    Col031 CHAR(1),
    Col032 CHAR(1),
    Col033 CHAR(1),
    Col034 CHAR(1),
    Col035 CHAR(1),
    Col036 CHAR(1),
    Col037 CHAR(1),
    Col038 CHAR(1),
    Col039 CHAR(1),
    Col040 CHAR(1),
    Col041 CHAR(1),
    Col042 CHAR(1),
    Col043 CHAR(1),
    Col044 CHAR(1),
    Col045 CHAR(1),
    Col046 CHAR(1),
    Col047 CHAR(1),
    Col048 CHAR(1),
    Col049 CHAR(1),
    Col050 CHAR(1),
    Col051 CHAR(1),
    Col052 CHAR(1),
    Col053 CHAR(1),
    Col054 CHAR(1),
    Col055 CHAR(1),
    Col056 CHAR(1),
    Col057 CHAR(1),
    Col058 CHAR(1),
    Col059 CHAR(1),
    Col060 CHAR(1),
    Col061 CHAR(1),
    Col062 CHAR(1),
    Col063 CHAR(1),
    Col064 CHAR(1),
    Col065 CHAR(1),
    Col066 CHAR(1),
    Col067 CHAR(1),
    Col068 CHAR(1),
    Col069 CHAR(1),
    Col070 CHAR(1),
    Col071 CHAR(1),
    Col072 CHAR(1),
    Col073 CHAR(1),
    Col074 CHAR(1),
    Col075 CHAR(1),
    Col076 CHAR(1),
    Col077 CHAR(1),
    Col078 CHAR(1),
    Col079 CHAR(1),
    Col080 CHAR(1),
    Col081 CHAR(1),
    Col082 CHAR(1),
    Col083 CHAR(1),
    Col084 CHAR(1),
    Col085 CHAR(1),
    Col086 CHAR(1),
    Col087 CHAR(1),
    Col088 CHAR(1),
    Col089 CHAR(1),
    Col090 CHAR(1),
    Col091 CHAR(1),
    Col092 CHAR(1),
    Col093 CHAR(1),
    Col094 CHAR(1),
    Col095 CHAR(1),
    Col096 CHAR(1),
    Col097 CHAR(1),
    Col098 CHAR(1),
    Col099 CHAR(1),
    Col100 CHAR(1)
);
```

### Data Insertion

Next, the script uses a `WHILE` loop to insert 100 rows into the table. Each row contains the character 'A' in all 100 columns.

```sql
use [0_MIKE_TEST_DB]
DECLARE @i INT = 1;
WHILE @i <= 100
BEGIN
    INSERT INTO Table_with_100_columns_n_100_rows (Col001, Col002, Col003, Col004, Col005, Col006, Col007, Col008, Col009, Col010, Col011, Col012, Col013, Col014, Col015, Col016, Col017, Col018, Col019, Col020, Col021, Col022, Col023, Col024, Col025, Col026, Col027, Col028, Col029, Col030, Col031, Col032, Col033, Col034, Col035, Col036, Col037, Col038, Col039, Col040, Col041, Col042, Col043, Col044, Col045, Col046, Col047, Col048, Col049, Col050, Col051, Col052, Col053, Col054, Col055, Col056, Col057, Col058, Col059, Col060, Col061, Col062, Col063, Col064, Col065, Col066, Col067, Col068, Col069, Col070, Col071, Col072, Col073, Col074, Col075, Col076, Col077, Col078, Col079, Col080, Col081, Col082, Col083, Col084, Col085, Col086, Col087, Col088, Col089, Col090, Col091, Col092, Col093, Col094, Col095, Col096, Col097, Col098, Col099, Col100)
    VALUES ('A', 'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A',  'A');
    SET @i = @i + 1;
END;
```

This loop runs from `@i = 1` to `@i = 100`, inserting a row with 'A' in every column during each iteration.

### Test Output

```sql
SELECT * FROM [0_MIKE_TEST_DB].[dbo].[Table_with_100_columns_n_100_rows]
```

![image](https://github.com/user-attachments/assets/733f9e82-7176-432f-b823-d68c2a693795)
