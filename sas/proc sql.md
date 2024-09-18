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

# group by and filter using PROC SQL IN SAS but also limiting the observations

```sql
proc SQL outobs=10 ;

create table test as

SELECT 	
	column1, column2, SUM(total_something) 
FROM 
(
select 
column1, 
column2, 
MONTH(column3) as somename,
/*MONTH(column4) as somedate,*/
COUNT(column5) as total_something
from LIBREF.TABLE

WHERE 
MONTH(column4) IN (4,5,6)

GROUP BY 
1,2,3
)
GROUP BY 1,2
```
