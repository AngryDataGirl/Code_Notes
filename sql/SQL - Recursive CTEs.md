
 

there are also non-recursive and recursive CTEs, the latter really unlocks the power of CTEs and are useful when processing hierarchical structures such as trees and graphs

  
  

## Syntax

```sql

WITH RECURSIVE cte_name AS
(
  CTE_auxiliary_query_1   -- non-recursive term
  UNION [ALL]
  CTE_auxiliary_query_2   -- recursive term
)

CTE_primary_query;

```

## Example 1: generating numbers 1 through 10

```sql

WITH RECURSIVE nums_consecutive AS
(
  SELECT 1 AS num
  UNION ALL
  SELECT num + 1 FROM nums_consecutive WHERE num < 10
)

SELECT * FROM nums_consecutive;

```

which generates
```
+------+
| num  |
+------+
|    1 |
|    2 |
|    3 |
|    4 |
|    5 |
|    6 |
|    7 |
|    8 |
|    9 |
|   10 |
+------+
```

## Example 2: Generating sequential numbers fitting a certain pattern


```SQL 
WITH RECURSIVE seq_nums AS (
  SELECT
    5 AS num,
    0 AS iteration
  UNION ALL
  SELECT
    (2 * num + num),
    iteration + 1
  FROM
    seq_nums
  WHERE
    iteration < 5
) SELECT * FROM seq_nums;
```

generates 

```
+------+-----------+
| num  | iteration |
+------+-----------+
|    5 |         0 |
|   15 |         1 |
|   45 |         2 |
|  135 |         3 |
|  405 |         4 |
| 1215 |         5 |
+------+-----------+
```


## Example 3: Finding the sum of the first 100 consecutive positive integers
```
WITH RECURSIVE nums_consecutive AS (
  SELECT 1 AS num
  UNION ALL
  SELECT num + 1 FROM nums_consecutive WHERE num < 100
) SELECT SUM(num) AS total_sum FROM nums_consecutive;
```

Result set:

```
+-----------+
| total_sum |
+-----------+
|      5050 |
+-----------+
```

## Example 4: Generating the first 15 Fibonacci numbers

The following is a somewhat more complicated usage of `WITH RECURSIVE`:

```
WITH RECURSIVE fib_table (FibBuilder, FibNum, FibIndex) AS (
  SELECT 1, 0, 0
  UNION ALL
  SELECT FibNum, FibNum + FibBuilder, FibIndex + 1 FROM fib_table WHERE FibIndex < 15
)
SELECT FibBuilder, FibNum, FibIndex FROM fib_table;
```

The result set:

```
+------------+--------+----------+
| FibBuilder | FibNum | FibIndex |
+------------+--------+----------+
|          1 |      0 |        0 |
|          0 |      1 |        1 |
|          1 |      1 |        2 |
|          1 |      2 |        3 |
|          2 |      3 |        4 |
|          3 |      5 |        5 |
|          5 |      8 |        6 |
|          8 |     13 |        7 |
|         13 |     21 |        8 |
|         21 |     34 |        9 |
|         34 |     55 |       10 |
|         55 |     89 |       11 |
|         89 |    144 |       12 |
|        144 |    233 |       13 |
|        233 |    377 |       14 |
|        377 |    610 |       15 |
+------------+--------+----------+
```


## Example 5: generating dates
as seen in this question https://leetcode.com/problems/friday-purchases-ii/

```sql
WITH RECURSIVE nov_fridays AS

(

    SELECT '2023-11-03' AS purchase_date
    UNION ALL
    SELECT DATE_ADD(purchase_date, INTERVAL 7 DAY) AS purchase_date
    FROM nov_fridays
    WHERE purchase_date < '2023-11-24'
)
```

| week_of_month | purchase_date |
| ---- | ---- |
| 1 | 2023-11-03 |
| 2 | 2023-11-10 |
| 3 | 2023-11-17 |
| 4 | 2023-11-24 |


## Example 6: generating dates - weeks and years

```sql
WITH everyweek (event_year, event_week) AS (
    SELECT
        2023 AS event_year,
        1 AS event_week
    FROM dual
    UNION ALL
    SELECT
--        event_year + 1 ,
--        event_week + 1 
        event_year + CASE WHEN event_week = 52 THEN 1 ELSE 0 END,
        CASE WHEN event_week = 52 THEN 1 ELSE event_week + 1 END
    FROM everyweek
    WHERE event_year <= 2024 and event_week <= 52
)

SELECT event_year,event_week
--, week_number
FROM everyweek
ORDER BY event_year,event_week
--, week_number;
;
```

**References:**
- [https://dev.mysql.com/doc/refman/8.0/en/with.html](https://dev.mysql.com/doc/refman/8.0/en/with.html)
- [https://leetcode.com/discuss/study-guide/1600722/database-sql-primer-part-3-common-table-expressions-ctes](https://leetcode.com/discuss/study-guide/1600722/database-sql-primer-part-3-common-table-expressions-ctes)
- [https://leetcode.com/discuss/study-guide/1601295/database-sql-primer-part-4-recursive-ctes](https://leetcode.com/discuss/study-guide/1601295/database-sql-primer-part-4-recursive-ctes)
