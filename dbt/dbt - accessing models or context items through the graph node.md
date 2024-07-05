#Reference  #CodeSnippet #Programming #dbt 

https://docs.getdbt.com/reference/dbt-jinja-functions/graph#:~:text=The%20graph%20context%20variable%20is%20a%20dictionary%20which,node%20ids%20onto%20dictionary%20representations%20of%20those%20nodes.

#dbt #Macros  

```sql

{% if execute %}
  {% for node in graph.nodes.values()
     | selectattr("resource_type", "equalto", "model")
     | selectattr("package_name", "equalto", "snowplow") %}
    {% do log(node.unique_id ~ ", materialized: " ~ node.config.materialized, info=true) %}
  {% endfor %}
{% endif %}
```

- the join is to concatenate the separate tags to strings separated by a blank space

- note that, we still need to give each element single quotes  

```
{% macro get_models_with_tag(tag) %}
{% if execute 
{% set models_with_tag = [] %}

{% for model in graph.nodes.values() | selectattr("resource_type", "equalto", "model") %}

    {% if tag in model.config.tags %}
        {{ models_with_tag.append(model.name) }}
    {% endif %}

{% endfor %}

{{ return(models_with_tag|join(',')) }}

{% endif %}

{% endmacro %}
```