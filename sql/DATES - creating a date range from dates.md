```sql
WITH min_max_dates AS (
    SELECT 
        MIN(EVENT_DATE) AS min_date,
        MAX(EVENT_DATE) AS max_date 
    FROM STG_IP_LOG
)
, all_days AS
(
SELECT
  (to_date(min_date,'DD-MM-YYYY') + level + 1) AS calendar_day
FROM
  min_max_dates
CONNECT BY LEVEL <= (to_date(max_date,'DD-MM-YYYY') - to_date(min_date,'DD-MM-YYYY') + 1)
)

SELECT 
    calendar_day,
    EXTRACT(YEAR from calendar_day) as calendar_year,
    EXTRACT(MONTH from calendar_day) as calendar_month,
    EXTRACT(DAY from calendar_day) as calendar_day,
    
    TO_NUMBER(TO_CHAR(calendar_day, 'WW')) AS event_week,    
    TRUNC(calendar_day, 'iw') AS iso_week_start_date, 
    TRUNC(calendar_day, 'iw') + 7 - 1/86400 AS iso_week_end_date
FROM all_days
```