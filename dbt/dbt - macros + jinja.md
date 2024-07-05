#CodeSnippet #Reference  


Example of #dbt generic #dbt/Test using #jinja control flow (if/then)

```sql

{% test test_name(model, column_name, custom_col1, custom_col2) %}

  {% if run_query("[SELECT * FROM model statement]") == 0 %}
  SELECT * FROM statement1
  {% else %}
  SELECT * FROM statement2
  {% endif %}

{% endtest %}

```

- actually this might not work since the run-query will return a <b>table</b>, and you are evaluating it against a single value
- the below code returns proper flow / results
- note the use of the print statement see [[dbt - print output when scripting with macros]]

```sql

{% set test_query %}


SELECT count(*)
FROM
(
SELECT *
WHERE
    table_name = 'table_name'
    AND column_name = 'column_name'
)  

{% endset %}

{% set results = run_query(test_query) %}
  
{% if execute %}
{# Return the first column #}
{% set results_list = results.columns[0].values() %}
{% else %}
{% set results_list = [] %}
{% endif %}

{{ print(results) }}
{{ print(results_list[0]) }}
  
{% if results_list[0] != 0 %}

SELECT 'not equal to zero' as x FROM dual

{% else %}
  
SELECT 'zero' as x FROM dual
  
{% endif %}

  

```

- you also want to take note of '' and "  ''  "
- in the example below, I have a generic test where I am passing in the model to the test-query -- which we will run and return a count
- if you don't set your quotations properly, the model might still run, but you will not get the intended results bc the if / then flow statement is not triggering as the comparison is empty
- then it turns out that dbt is returning a combination of my schema & table name, which it cannot find in the DB, ie 'USERNMAE.test_table' and it's not that that doesn't exist as a table, but that that is not how the information is stored on the USER_TAB_COLUMNS.
- thankfully, I found this https://docs.getdbt.com/reference/dbt-jinja-functions/model, you can do <b>{{ model.name }}</b>

```sql
{% test test_column_null_values(model, column_name, date_column) %}

{{ config(severity = 'warn') }}

{% set test_query %}

SELECT count(*)
FROM
(

SELECT column_name, table_name FROM USER_TAB_COLUMNS
WHERE
    table_name = '{{ model.name }}'
    AND column_name = 'COLUMN NAME'
)  

{% endset %}
```


## What if the IF statement depends on a dynamic model?

- ie, you want to feed it a variable that may change in the jinja

- there migh be a smarter way to make sure it compiles & without a macro, but I thought it would be good to have the sql query run as a macro, where it is super simple to sub in the variable that will change

- then call that macro in the if statement

- note that in this example the changing variable was 'model' and 'model' is also one of the default arguments for a custom generic test

- the if statement required a sql statement, where I am checking if the column exists on a particular table

- this would also be used on other tables, which is why I need to sub in the {{model}}

- this documentation was important to know why it was running into compile errors (and more difficult to have the query pasted into the {{if block}} of the jinja statement [https://docs.getdbt.com/docs/building-a-dbt-project/dont-nest-your-curlies]

  

### the macro

```sql

{% macro check_if_column_exists(column_name, model) %}

  

 SELECT CASE WHEN count(*) = 0 THEN 'FALSE' ELSE 'TRUE' END AS column_existence

    FROM (

        SELECT column_name, table_name FROM USER_TAB_COLUMNS

        WHERE

            table_name = {{ model }}

            AND column_name = {{ column_name }}

            )

  

{% endmacro %}

```

### the if statement in the test

```sql

{% if check_if_column_exists('column_name','model') == 'TRUE' %} #calling the macro

  

SELECT *    

FROM {{ model }} #this is the same model variable

WHERE ...

{% else %}

  

SELECT *

FROM {{ model }}

WHERE ...

  

{% endif %}

  

{% endtest %}

```


**References:**

- Official Documentation on Jinja and Macros: [https://docs.getdbt.com/docs/build/jinja-macros]
- Really good tutorial on Jinja: [https://ttl255.com/jinja2-tutorial-part-2-loops-and-conditionals/]
