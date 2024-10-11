```sql
FROM TABLE_A A
LEFT JOIN TABLE_B B B ON 
    B.pri = B.pri 
    AND A.date_field =
        CASE WHEN A.date_field = B.match_this_field THEN b.return_this
            ELSE B.other_field
            END
    AND rn=1 /*random condition*/
```
