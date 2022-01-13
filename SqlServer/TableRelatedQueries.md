## Get Number of Rows for all the tables
```sql
    select SCHEMA_NAME(t.schema_id) as SchemaName,  t.name as TableName, 
    p.rows
    from sys.tables t 
    inner join sys.partitions p
    on t.object_id = p.object_id
```

## Check whether a table is Heap or B tree
```sql
    select 
	SCHEMA_NAME(t.schema_id) as SchemaName,
    o.name as TableName, 
    case 
      when p.index_id = 0 then 'Heap'
      when p.index_id = 1 then 'Clustered Index/b-tree'
      when p.index_id > 1 then 'Non-clustered Index/b-tree'
    end as 'Type',
	p.rows as NumberOfRows
    from sys.objects o
    inner join sys.partitions p on p.object_id = o.object_id
    inner join sys.tables t on t.object_id = o.object_id
```
## File and Page numbers for tables
[Good Refresher on Pages types](http://www.sqlnotes.info/2011/10/31/page-type/)
```sql
 	Select allocated_page_file_id as PageFID, allocated_page_page_id as PagePID,
	object_id as ObjectID, partition_id as PartitionID,
	allocation_unit_type_desc as AU_type, page_type as PageType,
	extent_file_id, extent_page_id, is_mixed_page_allocation
	from sys.dm_db_database_page_allocations(db_id('dp300'),object_id('SalesLT.SalesOrderHeaderCopy') , null, null, 'DETAILED')
    Where page_type = 1; --Data page
    -- where page_type = 2; --Index page
    -- where page_type = 8; --GAM Page
    -- where page_type = 9; --SGAM page
    -- where page_type = 10; --IAM page
    -- where page_type = 11; --PFS page
```
