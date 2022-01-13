# Get Number of Rows for all the tables
```sql
    select SCHEMA_NAME(t.schema_id) as SchemaName,  t.name as TableName, 
    p.rows
    from sys.tables t 
    inner join sys.partitions p
    on t.object_id = p.object_id
```