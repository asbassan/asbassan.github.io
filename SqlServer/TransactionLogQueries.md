## Get the used space in T logs for a database
```sql
    SELECT total_log_size_in_bytes*1.0/1024/1024 total_log_size_in_MB,
	used_log_space_in_bytes*1.0/1024/1024 used_log_space_in_MB,
	(total_log_size_in_bytes - used_log_space_in_bytes)*1.0/1024/1024
	AS free_log_space_in_MB,
	used_log_space_in_percent
    FROM sys.dm_db_log_space_usage;
```