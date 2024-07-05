
#Oracle
## add a column to your table

```sql
ALTER TABLE my_table ADD (new_col DATE);
```
## modify old column value  

Set this new column's value to hold the old_column's value converted to a DATE value.

```sql
UPDATE my_table SET new_col=TO_DATE(old_col,'MM/DD/YYYY');
```
Update format mask as needed.
## drop the old column.

```sql
ALTER TABLE my_table DROP (old_col);
```
## rename new column to old column

```sql
ALTER TABLE my_table RENAME new_col TO old_col;
```

  