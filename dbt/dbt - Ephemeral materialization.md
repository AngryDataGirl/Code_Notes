#dbt #Ephemeral #IncrementalMaterializations 
[Best practices for materializations | dbt Developer Hub (getdbt.com)](https://docs.getdbt.com/best-practices/materializations/5-best-practices)

🔑 **Golden Rule of Materializations** Start with models as views, when they take too long to query, make them tables, when the tables take too long to build, make them incremental.

### Ephemeral[​](https://docs.getdbt.com/docs/build/materializations#ephemeral "Direct link to Ephemeral")

`ephemeral` models are not directly built into the database. Instead, dbt will interpolate the code from this model into dependent models as a common [table](https://docs.getdbt.com/terms/table) expression.

- **Pros:**
    - You can still write reusable logic
    - Ephemeral models can help keep your [data warehouse](https://docs.getdbt.com/terms/data-warehouse) clean by reducing clutter (also consider splitting your models across multiple schemas by [using custom schemas](https://docs.getdbt.com/docs/build/custom-schemas)).
- **Cons:**
    - You cannot select directly from this model.
    - [Operations](https://docs.getdbt.com/docs/build/hooks-operations#about-operations) (for example, macros called using [`dbt run-operation`](https://docs.getdbt.com/reference/commands/run-operation) cannot `ref()` ephemeral nodes)
    - Overuse of ephemeral materialization can also make queries harder to debug.
    - Ephemeral materialization doesn't support [model contracts](https://docs.getdbt.com/docs/collaborate/govern/model-contracts#where-are-contracts-supported).
- **Advice:** Use the ephemeral materialization for:
    - very light-weight transformations that are early on in your DAG
    - are only used in one or two downstream models, and
    - do not need to be queried directly