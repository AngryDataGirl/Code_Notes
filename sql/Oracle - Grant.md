#Oracle #Oracle/Grant

>[!Tip]
> No comma needed around username! 
## **GRANT**

```sql
GRANT SELECT ON tablename TO username;
```
## **WITH GRANT OPTION**
- When receiving error ORA-01720: grant option does not exist for 'table_name'

```sql
GRANT SELECT ON schema.table_name TO username WITH GRANT OPTION;
```
## **GRANT CREATE VIEW**

```sql
GRANT CREATE ANY VIEW TO username;
```

  