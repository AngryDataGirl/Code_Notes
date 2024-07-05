#Oracle 
#Connections

# find #Server

```
SELECT sys_context('USERENV','SERVER_HOST') FROM dual
```
# find  #ServiceName

Helpful for trying to find the connection information required to set up other connections (ie, through python) or some dashboard software like POWER BI.

```sql
select * from global_name;
```
# find #Tables

Helpful when trying to:
- understand what tables or v iews are within a schema
- find table names or view names within a schema

```sql
SELECT *
FROM all_tables;
```

# find #Views

```sql
SELECT view_name
FROM user_views;
```

# list all #DatabaseLinks


```sql
DBA_DB_LINKS - All DB links defined in the database
ALL_DB_LINKS - All DB links the current user has access to
USER_DB_LINKS - All DB links owned by current user
```

# list functions, #Procedures and packages

```sql
SELECT *
FROM ALL_OBJECTS
WHERE OBJECT_TYPE IN ('FUNCTION','PROCEDURE','PACKAGE')
```
# find all #indexes <a name = "indexes"></a>

```sql

SELECT *

FROM all_indexes

-- WHERE owner = 'user'

```


# Datatypes <a name = "datatypes"></a>

  

## datatype codes

https://docs.oracle.com/cd/A58617_01/server.804/a58234/datatype.htm

  

| Internal Oracle Datatype| Maximum Internal Length | Datatype Code |

| ----|----|----|

|VARCHAR2  |4000 bytes  |1  |

|NUMBER    |21 bytes    |2 |

|DATE    |7 bytes    |12   |

|CHAR  |2000 bytes  |96  |

|RAW  |2000 bytes |23|  

# Strings <a name = "strings"></a>

  

## apostrophes within strings

  

[Oracle / PLSQL: Dealing with apostrophes/single quotes in strings (techonthenet.com)](https://www.techonthenet.com/oracle/questions/quotes.php#:~:text=Answer%3A%20Now%20it%20is%20first%20important%20to%20remember,where%20the%20quote%20is%20located%20in%20the%20string.)

  

**Question:** How can I handle apostrophes and single quotes in strings? As you know, single quotes start and terminate strings in SQL.

  

**Answer:** Now it is first important to remember that in Oracle, you enclose strings in single quotes. The first quote denotes the beginning of the string and the second quote denotes the termination of the string.

  

If you need to deal with apostrophes/single quotes in strings, your solution depends on where the quote is located in the string.

  

We'll take a look at 4 scenarios where you might want to place an apostrophe or single quote in a string.

  

## **Apostrophe/single quote at start of string**

  

When the apostrophe/single quote is at the start of the string, you need to enter 3 single quotes for Oracle to display a quote symbol. For example:

  

```

SELECT '''Hi There'

FROM dual;

```

  

would return

  

```

'Hi There

```

  

## **Apostrophe/single quote in the middle of a string**

  

When the apostrophe/single quote is in the middle of the string, you need to enter 2 single quotes for Oracle to display a quote symbol. For example:

  

```

SELECT 'He''s always the first to arrive'

FROM dual;

```

  

would return

  

```

He's always the first to arrive

```

  

## **Apostrophe/single quote at the end of a string**

  

When the apostrophe/single quote is at the end of a string, you need to enter 3 single quotes for Oracle to display a quote symbol. For example:

  

```

SELECT 'Smiths'''

FROM dual;

```

  

would return

  

```

Smiths'

```

  

## **Apostrophe/single quote in a concatenated string**

  

If you were to concatenate an apostrophe/single quote in a string, you need to enter 4 single quotes for Oracle to display a quote symbol. For example:

  

```

SELECT 'There' || '''' || 's Henry'

FROM dual;

```

  

would return

  

```

There's Henry

```

  

## susbtring

https://docs.oracle.com/database/121/SQLRF/functions196.htm#SQLRF06114

  

```sql

SUBSTR( str, start_position [, substring_length, [, occurrence ]] );

```

The SUBSTR() function accepts three arguments:

- str: STR that you want to extract the substring from. The data type of str can be CHAR, VARCHAR2, NCHAR, NVARCHAR2, CLOB, or NCLOB.

- start_position: INT that determines where the substring starts.

    - 0, substring will start at first character of the str.

    - start_position is positive, the SUBSTR() function will count from the beginning of the str.

    - start_position is negative, then the SUBSTR() function will count backward from the end of the str .

- substring_length: the number of characters in the substring.

    - If omitted, the SUBSTR() function returns all characters starting from the start_position.

    - In case the substring_length is less than 1, the SUBSTR() function returns null.

## instring

https://docs.oracle.com/database/121/SQLRF/functions196.htm#SQLRF06114

  

```sql

SELECT INSTR('CORPORATE FLOOR','OR', 3, 2) "Instring"

  FROM DUAL;

  Instring

----------

        14

```

  

## reversed instring

```sql

SELECT INSTR('CORPORATE FLOOR','OR', -3, 2) "Reversed Instring"

  FROM DUAL;

Reversed Instring

-----------------

                2

```


# Loops

  

Handy Loop Logic templates to

- drop tables or views matching a certain critera

- create tables or views with a certain naming convention

- share tables or views / grant permissions

  

## Loop for creating views or tables

  

```sql

begin

    for x in (

        SELECT *

        FROM all_tables / all_views

        WHERE owner = 'OWNER_NAME' AND (

            table_name/view_name LIKE '%criteria1%'

            OR table_name/view_name LIKE '%criteria1%'

            OR table_name/view_name LIKE '%criteria1%'

            )

            )

    loop

        execute immediate 'CREATE VIEW '||x.table_name/x.view_name||' AS (SELECT * FROM '||x.owner||'.'|| x.table_name/x.view_name||')';

    end loop;

end;

```

  

## Loop for grant permissions

  

simple loop

```sql

begin

    for x in (select * from all_views/all_tables where owner = 'replace this with USER NAME 1 that owns table')

    loop

        execute immediate 'GRANT SELECT ON '||x.owner||'.'|| x.view_name || ' to ' || 'replace this with USER NAME that view is to be granted to';

    end loop;

end;

```

loop with criteria for matching table or view names

```sql

begin

    for x in (

        SELECT *

        FROM all_tables / all_views  

        WHERE owner = 'OWNER_NAME'

        AND table_name/view_name LIKE '%criteria1%'

        OR table_name/view_name LIKE '%criteria2%'

        OR table_name/view_name LIKE '%criteria3%'

    )

    loop

        execute immediate 'GRANT SELECT ON '||x.owner||'.'|| x.table_name/x.view_name || ' to ' || 'USER YOU ARE GRANTING PERMISSIONS TO';

    end loop;

end;

```

  

## Loop for dropping tables

  

```sql

begin

  for i in (

    SELECT 'drop view '||table_name/view_name||' cascade constraints' tbl

    FROM user_views / user_tables / all_tables

    WHERE

     owner = 'AWENG'

--        OR

--        table_name LIKE '%something%'

--        OR

        view_name LIKE '%something%'

        )

  loop

     execute immediate i.tbl;

  end loop;

end;

```