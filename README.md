# SQL Null Checker

This project includes a SQL script to check for `NULL` values and the string `'NULL'` in each column of a specified table.

## SQL Script

The following script counts the occurrences of `NULL` and the string `'NULL'` in each column of a table.

### `CheckNullValues.sql`

```sql
DECLARE @TableName NVARCHAR(MAX) = 'TableName'; -- Your table name
DECLARE @SQL NVARCHAR(MAX) = '';

-- Generate SQL to count occurrences of NULL and 'NULL' string in each column
SELECT @SQL = STRING_AGG(
    'SELECT ''' + COLUMN_NAME + ''' AS ColumnName, ' +
    'SUM(CASE WHEN [' + COLUMN_NAME + '] IS NULL OR [' + COLUMN_NAME + '] = ''NULL'' THEN 1 ELSE 0 END) AS NullCount ' +
    'FROM [' + @TableName + ']',
    ' UNION ALL '
)
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = @TableName;

-- Execute the generated SQL
EXEC sp_executesql @SQL;

USE [world_layoffs_project]
GO

