WEEK
```sql
select 
    TRUNC(sysdate, 'iw') AS iso_week_start_date,
    TRUNC(sysdate, 'iw') + 7 - 1/86400 AS iso_week_end_date
from dual;
```
MONTH
```sql
select 
    TRUNC (sysdate, 'mm') AS month_start_date,
    LAST_DAY (TRUNC (sysdate, 'mm')) + 1 - 1/86400 AS month_end_date
from dual;
```