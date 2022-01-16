## Create Database scripts
[Reference](https://www.mssqltips.com/sqlservertip/6200/sql-server-create-database-examples/)
```sql
    -- create database MyDatabase and specify physical file locations, initial physical file sizes, and autogrowth increments, change owner to sa, and set recovery model to simple
 
    CREATE DATABASE [MyDatabase] 
        ON (NAME = N'MyDatabase', FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2017\MSSQL\DATA\MyDatabase.mdf', SIZE = 1024MB, FILEGROWTH = 256MB)
        LOG ON (NAME = N'MyDatabase_log', FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2017\MSSQL\DATA\MyDatabase_log.ldf', SIZE = 512MB, FILEGROWTH = 125MB)
    GO
    
    -- change owner to sa
    USE [MyDatabase]
    GO
    ALTER AUTHORIZATION ON DATABASE::[MyDatabase] TO [sa]
    GO
    
    -- set recovery model to simple 
    ALTER DATABASE [MyDatabase] SET RECOVERY SIMPLE 
    GO
```
## Create Table
[Reference](https://www.sqlservertutorial.net/sql-server-basics/sql-server-create-table/)
```sql
    CREATE TABLE [database_name.][schema_name.]table_name (
    pk_column data_type PRIMARY KEY,
    column_1 data_type NOT NULL,
    column_2 data_type,
    ...,
    table_constraints
    );
```

## Sql data types
[Reference](https://www.sqlservertutorial.net/sql-server-basics/sql-server-data-types/)

[Numeric and Decimal Data types Memory](https://docs.microsoft.com/en-us/sql/t-sql/data-types/decimal-and-numeric-transact-sql?view=sql-server-ver15)

*Decimal and numeric rounds to nearest 0*

## Arithmetic operators
[Reference](https://docs.microsoft.com/en-us/sql/t-sql/language-elements/arithmetic-operators-transact-sql?view=sql-server-ver15)

## Mathematical Functions
[Reference](https://docs.microsoft.com/en-us/sql/t-sql/functions/mathematical-functions-transact-sql?view=sql-server-ver15)







