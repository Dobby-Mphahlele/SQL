# SQL Null Checker

This project includes a stored procedure to check for `NULL` values in a table.

## Stored Procedure

The `CheckNullValues` stored procedure counts the occurrences of `NULL` in each column of a specified table.

### `CheckNullValues.sql`

```sql
CREATE PROCEDURE CheckNullValues
    @TableName NVARCHAR(MAX)
AS
BEGIN
    DECLARE @SQL NVARCHAR(MAX) = '';

    -- Generate SQL to count occurrences of NULL in each column
    SELECT @SQL = STRING_AGG(
        'SELECT ''' + COLUMN_NAME + ''' AS ColumnName, ' +
        'SUM(CASE WHEN [' + COLUMN_NAME + '] IS NULL THEN 1 ELSE 0 END) AS NullCount ' +
        'FROM [' + @TableName + ']',
        ' UNION ALL '
    )
    FROM INFORMATION_SCHEMA.COLUMNS
    WHERE TABLE_NAME = @TableName;

    -- Execute the generated SQL
    EXEC sp_executesql @SQL;
END;

