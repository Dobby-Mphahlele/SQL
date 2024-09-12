# SQL Null Checker

This project includes a stored procedure to check for `NULL` values in a table.

## How to Use

1. Run the `CheckNullValues.sql` script to create the stored procedure in your SQL Server.
2. Execute the stored procedure with:
   ```sql
   EXEC CheckNullValues 'YourTableName';
