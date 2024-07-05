# Group By and Filter using PROC SQL IN SAS

```sql
PROC SQL; 

SELECT 

fiscal_year, 
YEAR(DATE_FIELD) as year,
MONTH(DATE_FIELD) as month,
count(*)

FROM LIBREF.TABLE_NAME
WHERE FILTER_FIELD = SOME_NUMBER
GROUP BY 

1,2,3
;

QUIT;
```