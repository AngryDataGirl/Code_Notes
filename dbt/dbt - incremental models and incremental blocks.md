a
#dbt #IncrementalMaterializations 
https://docs.getdbt.com/docs/build/incremental-models
## When to use incremental models
- Source data has millions or billions of rows.
- Data transformations on the source data are computationally expensive (take a long time to execute) and complex, like using Regex or UDFs.
## Understanding the is_incremental() macro[​](https://docs.getdbt.com/docs/build/incremental-models#understanding-the-is_incremental-macro "Direct link to Understanding the is_incremental() macro")

The `is_incremental()` macro will return `True` if _all_ of the following conditions are met:

- the destination table already exists in the database
- dbt is _not_ running in full-refresh mode
- The running model is configured with `materialized='incremental'`

Note that the SQL in your model needs to be valid whether `is_incremental()` evaluates to `True` or `False`.

## using incremental materializations

```sql
{{  
config(  
materialized='incremental'  
)  
}}  
  
select ...
```

To use incremental models, you also need to tell dbt:

- How to filter the rows on an incremental run
- The unique key of the model (if any)

## filtering rows on an incremental run

To tell dbt which rows it should transform on an incremental run, wrap valid SQL that filters for these rows in the `is_incremental()` macro.

Often, you'll want to filter for "new" rows, as in, rows that have been created since the last time dbt ran this model. The best way to find the timestamp of the most recent run of this model is by checking the most recent timestamp in your target table. dbt makes it easy to query your target table by using the "[{{ this }}](https://docs.getdbt.com/reference/dbt-jinja-functions/this)" variable.

Also common is wanting to capture both new and updated records. For updated records, you'll need to [define a unique key](https://docs.getdbt.com/docs/build/incremental-models#defining-a-unique-key-optional) to ensure you don't bring in modified records as duplicates. Your `is_incremental()` code will check for rows created _or modified_ since the last time dbt ran this model.

For example, a model that includes a computationally slow transformation on a column can be built incrementally, as follows:

```sql
{{
    config(
        materialized='incremental'
    )
}}

select
    *,
    my_slow_function(my_column)

from raw_app_data.events

{% if is_incremental() %}

  -- this filter will only be applied on an incremental run
  -- (uses > to include records whose timestamp occurred since the last run of this model)
  where event_time > (select max(event_time) from {{ this }})

{% endif %}
```
