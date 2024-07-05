
#Concepts #SQL/WindowFunctions 

Window functions apply aggregate and ranking functions over a particular window (set of rows).
- `OVER` clause is used with window functions to define that window.
    - The `PARTITION`  is where you create the group
    - The `ORDER BY` clause orders rows within the partition / window into a particular order.
- if a partition is not provided, then `ORDER BY` will order all rows of table

Window functions are similar to the aggregation done in the GROUP BY clause.
- However, rows are not grouped into a single row, each row retains their separate identity even as you apply logic that sums a group. 
-  They are useful when you need to work with aggregate and non-aggregate values such as when you need to compare one value to an aggregate value on a single record (since the window function does not collapse the records together),   