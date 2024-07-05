
Lots of the models have incremental portions where the model will only update the data that is new based on the lookup key, ie below:

A `unique_key` enables updating existing rows instead of just appending new rows. If new information arrives for an existing `unique_key`, that new information can replace the current information instead of being appended to the table. If a duplicate row arrives, it can be ignored. Refer to [strategy specific configs](https://docs.getdbt.com/docs/build/incremental-models#strategy-specific-configs) for more options on managing this update behavior, like choosing only specific columns to update.

Not specifying a `unique_key` will result in append-only behavior, which means dbt inserts all rows returned by the model's SQL into the preexisting target table without regard for whether the rows represent duplicates.

The optional `unique_key` parameter specifies a field (or combination of fields) that define the grain of your model. That is, the field(s) identify a single unique row. You can define `unique_key` in a configuration block at the top of your model, and it can be a single column name or a list of column names.

The `unique_key` should be supplied in your model definition as a string representing a single column or a list of single-quoted column names that can be used together, for example, `['col1', 'col2', …])`. Columns used in this way should not contain any nulls, or the incremental model run may fail. Either ensure that each column has no nulls (for example with `coalesce(COLUMN_NAME, 'VALUE_IF_NULL')`), or define a single-column [surrogate key](https://docs.getdbt.com/terms/surrogate-key) (for example with [`dbt_utils.generate_surrogate_key`](https://github.com/dbt-labs/dbt-utils#generate_surrogate_key-source)).

When you define a `unique_key`, you'll see this behavior for each row of "new" data returned by your dbt model:

- If the same `unique_key` is present in the "new" and "old" model data, dbt will update/replace the old row with the new row of data. The exact mechanics of how that update/replace takes place will vary depending on your database, [incremental strategy](https://docs.getdbt.com/docs/build/incremental-models#about-incremental_strategy), and [strategy specific configs](https://docs.getdbt.com/docs/build/incremental-models#strategy-specific-configs).
- If the `unique_key` is _not_ present in the "old" data, dbt will insert the entire row into the table.
- 
```sql
{{
    config(
        materialized='incremental',
        unique_key='date_day'
    )
}}

select
    date_trunc('day', event_at) as date_day,
    count(distinct user_id) as daily_active_users

from raw_app_data.events


{% if is_incremental() %}

  -- this filter will only be applied on an incremental run
  -- (uses >= to include records arriving later on the same day as the last run of this model)
  where date_day >= (select max(date_day) from {{ this }})

{% endif %}

group by 1
```
