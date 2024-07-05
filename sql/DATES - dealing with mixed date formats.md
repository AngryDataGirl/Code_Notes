# DATES, TIMESTAMPS 

# Mixed date formats stored as strings
- mixed date formats stored as strings
- how to format all in same column and address literal error?
- `EVENT_DATE` is the string date with mixed formats in this example  
- use `DEFAULT NULL ON CONVERSION ERROR` argument in the conversion function , in this case it is `TO_DATE`
  
```sql
SELECT 
    CASE 
        WHEN TO_DATE(EVENT_DATE DEFAULT NULL ON CONVERSION ERROR,'YYYY/MM/DD') IS NOT NULL THEN TO_DATE(EVENT_DATE,'YYYY/MM/DD') 
        WHEN TO_DATE(EVENT_DATE DEFAULT NULL ON CONVERSION ERROR,'DD/MM/YYYY') IS NOT NULL THEN TO_DATE(EVENT_DATE,'MM/DD/YYYY') 
    ELSE NULL
    END as new_column_name 
FROM TABLE_NAME 
```