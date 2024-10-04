```sql
-- Tables + Size MB
select owner, table_name, round((num_rows*avg_row_len)/(1024*1024)) MB 
from all_tables 
where owner not like 'SYS%'  -- Exclude system tables.
AND owner like '%AWENG%'
and num_rows > 0  -- Ignore empty Tables.
order by MB desc -- Biggest first.
;
```
