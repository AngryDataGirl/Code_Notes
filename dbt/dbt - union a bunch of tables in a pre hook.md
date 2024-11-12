
this is some basic template where:

1. checks if table name is equal to x 
2. it counts it
3. if the count is greater than 0, add a column calls table exists as a NULL INT

this model will:

pre hook : collect all test tables and union them into a temp table

create new table TEST_FAILURES_i which stands for test failures individual (as it returns individual pris, emp stat id and the test name where it failed)

post hook :

1. drops the test tables as the results are now in this single table
2. drops the temp table

```sql
{{
    config(
        materialized='incremental',
        unique_key=['col1','col2','col_name_holding_table_name'], 
        pre_hook = [
            
        "DECLARE i INTEGER;
            BEGIN
                SELECT COUNT(*) INTO i
                FROM user_tables WHERE table_name IN ('TEMP_TABLE');
            IF i > 0 
            THEN 
                EXECUTE IMMEDIATE ('DROP TABLE TEMP_TABLE');
            END IF; END;",
            "
DECLARE    tests  VARCHAR2 (10000);
    BEGIN
       FOR cur_r IN (SELECT object_name
                       FROM user_objects
                      WHERE     object_type = 'TABLE'
                            AND object_name LIKE 'TEST_COLUMN%') --Change this to your test suffix (Currently set to TEST1%)
       LOOP
          tests :=
            tests || ' select DISTINCT pri, col1, col2, '''|| cur_r.object_name ||''' as col_name_holding_table_name from ' || cur_r.object_name || ' union all ';
      END LOOP;
      tests :=
            'create table TEMP_TABLE as ' --change the table name here (Currently set to TEST_JOINS)
         || RTRIM (tests, ' union all');
      EXECUTE IMMEDIATE tests;
   END;
   "],
        post_hook=["
BEGIN
  FOR rec IN
    (SELECT table_name FROM user_tables WHERE table_name LIKE '%TEST_COLUMN%') 
    LOOP EXECUTE immediate 'DROP TABLE  '||rec.table_name; END LOOP;
END;
        ", 
        
        "DECLARE i INTEGER;
            BEGIN
                SELECT COUNT(*) INTO i
                FROM user_tables WHERE table_name IN ('TEMP_TABLE');
            IF i > 0 
            THEN 
                EXECUTE IMMEDIATE ('DROP TABLE TEMP_TABLE');
            END IF; END;"
        ]
    )
}}



SELECT * FROM TEMP_TABLE

{% if is_incremental() %}

WHERE pri||col1||col2||col_name_holding_table_name 
NOT IN (
    select pri||col1||col2||col_name_holding_table_name from {{this}}
    )

{% endif %}
```
