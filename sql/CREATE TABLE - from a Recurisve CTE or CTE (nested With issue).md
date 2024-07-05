This is a code snippet showing the format with which you can create a table with a #recursiveCTE (since if you're not careful it will complain about nested WITHs) in #Oracle

```sql
CREATE TABLE employee_hierarchy AS
WITH recursive employee_hierarchy AS (
    SELECT
        employee_id,
        manager_id,
        employee_name,
        1 AS level
    FROM employees
    WHERE manager_id IS NULL -- Base case: top-level managers

    UNION ALL

    SELECT
        e.employee_id,
        e.manager_id,
        e.employee_name,
        eh.level + 1
    FROM employees e
    JOIN employee_hierarchy eh ON e.manager_id = eh.employee_id
)
SELECT * FROM employee_hierarchy;
```