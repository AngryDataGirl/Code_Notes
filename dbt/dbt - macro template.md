
# macro template

SQL + jinja 

```sql
{% macro macro_name(arg1,arg2) %}

SELECT 
    * 
FROM STG_WORK_ARRGMNT

{% endmacro %}


```

# using macro in model

```
 {{ macro_name('') }}
```