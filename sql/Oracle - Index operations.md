# creating #index

```sql
create index <index_name> on <table_name> ( <column1>, <column2>, … );
```

# dropping #index

```sql
DROP INDEX [schema_name.]index_name;
```
  
## drop #index if it exists in #indexes

```sql
DECLARE index_count INTEGER;
BEGIN
SELECT COUNT(*) INTO index_count
    FROM USER_INDEXES
    WHERE INDEX_NAME = 'index_name';
IF index_count > 0 THEN
    EXECUTE IMMEDIATE 'DROP INDEX index_name';
END IF;
END;

```

  
