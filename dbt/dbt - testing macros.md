say you have a macro 

```sql
{% macro drop_index(index_name) %}

DECLARE
	i INTEGER;
BEGIN
	SELECT COUNT(*) INTO i FROM all_objects WHERE object_name = '{{ index_name }}' AND owner = '{{ var('user') }}';
	IF i > 0 THEN
	EXECUTE IMMEDIATE ('DROP INDEX {{ index_name }}'); END IF; END;

{% endmacro %}
```

you want to see how it compiles to figure out quotation marks and stuff 

create a dummy model like so 

```sql
{% set index_name = "INDEX_ENTRY" %}

{{
    config(
        materialized='table'
    )
}}

{{drop_index(index_name)}}

{{create_index(index_name,'col1')}}

```

- note that we can set variables if need to be reused using
`{% set index_name = "INDEX_ENTRY" %}`

then run `dbt compile` 
and it will print the compiled sql so you can see if quotation marks are missing 
