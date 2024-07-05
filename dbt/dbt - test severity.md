#CodeSnippet #Reference 
#dbtTests 
 
The relevant configs are:

- `severity`: error or warn (default: error)
- `error_if`: conditional expression (default: !=0)
- `warn_if`: conditional expression (default: !=0)

Note that each of these configs need to be wrapped in their own config {{}} like this

```YAML
{{ config(severity = 'warn') }}
{{ config(warn_if = '>=1') }}
```
### project level test severity

```yaml
tests:
  +severity: warn  # all tests

  <package_name>:
    +warn_if: >10 # tests in <package_name>
```
### test severity on OOB generic model

However I found that this actually works for the custom generic tests as well and that the example of the custom generic actually does not work

```yml
models:
  - name: large_table
    columns:
      - name: slightly_unreliable_column
        tests:
          - unique:
              config:
                severity: error
                error_if: ">1000"
                warn_if: ">10"
```
### test severity on singular model

While it is sorta implied in the contextual text before the examples, note that in the offical documentation the singular test example is simply:

```yaml
{{ config(error_if = '>50') }}
```

This will not apply if you do not also add a config line on the singular model to tell it which severity to check for. So your test severity config block at the beginning of your file needs to look like this:
  
```yaml
{# singular test severity : warn #}
{{ config(severity = 'error') }}
{{ config(error_if = '>=1') }}
```

or like this 

```YAML 
{# singular test severity : error #}
{{ config(severity = 'warn') }}
{{ config(warn_if = '>=1') }}
```


**References:**
Official Documentation: [https://docs.getdbt.com/reference/resource-configs/severity]