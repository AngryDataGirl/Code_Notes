#Oracle 
#DesignPattern 

To find **all tables with a particular column** when you know the column name:

```sql 
SELECT * 
FROM ALL_TAB_COLUMNS
WHERE 
    COLUMN_NAME LIKE '%COLUMN_NAME%'
    AND OWNER LIKE '%OWNER_NAME%';
```

```sql
select 
	owner, 
	table_name
from all_tab_columns 
where column_name = 'ID';
```

To find tables that have **any or all** of the 4 columns:

```sql
select owner, table_name, column_name
from all_tab_columns
where column_name in ('ID', 'FNAME', 'LNAME', 'ADDRESS');
```

To find tables that have **all 4 columns (with none missing)**:

```sql
select owner, table_name
from all_tab_columns
where column_name in ('ID', 'FNAME', 'LNAME', 'ADDRESS')
group by owner, table_name
having count(*) = 4;
```

