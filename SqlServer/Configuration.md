## Azure SQL Get configuration
[Reference](https://docs.microsoft.com/en-us/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database?view=azure-sqldw-latest)
```sql
    SELECT  d.name,   
        slo.*    
    FROM sys.databases d   
    JOIN sys.database_service_objectives slo    
    ON d.database_id = slo.database_id;
```