# What is a CTE?

A CTE is a named subquery that appears at the top of a query in a WITH clause, which can contain multiple CTEs separated by commas.


# Benefits of using CTEs
<br> The benefits of a CTE are:
- makes queries more readable by organizing long / complex queries with multiple steps
- CTEs can be reused, CTE can refer to any other CTE defined above it in the same WITH clause
# Syntax:

```sql

WITH cte1 AS
(
  query_block
)
,
cte2 AS
(
  query_block
)

SELECT *
FROM cte1
LEFT JOIN cte2
  ON cte1.something = cte2.something

```

  
