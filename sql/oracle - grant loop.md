```sql
begin
    for x in (select * from all_views/all_tables where owner = 'replace this with USER NAME 1 that owns table')
    loop
        execute immediate 'GRANT SELECT ON '||x.owner||'.'|| x.view_name || ' to ' || 'replace this with USER NAME that view is to be granted to';
    end loop;
end;
```

