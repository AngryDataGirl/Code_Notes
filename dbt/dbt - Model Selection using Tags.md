#dbt #Code #Reference #dbtTesting
#CodeSnippet 

https://docs.getdbt.com/reference/node-selection/test-selection-examples

Run tests on a model (indirect selection) / upstream / downstream

```python
$ dbt test --select customers / +stg_customers / stg_customers+
```

Run tests on all models with a particular tag (direct + indirect) - note that tag has to be set on the model in the yaml config 

```Python
$ dbt test --select tag:my_model_tag
```

Run tests on all models with a particular tag,  multi tags selection USE COMMA NO SPACES

```Python
$ dbt run --select tag:my_model_tag1,tag:my_model_tag2
```

```python

# singular / generic

$ dbt test --select test_type:singular / generic

# directly select the test by name
$ dbt test --select (test_name)

# other test selection
dbt test --select "assert_total_payment_amount_is_positive" 

# directly select the test by name
dbt test --select "payments,test_type:singular" 

# indirect selection, v1.2
dbt test --select "payments,test_type:data" 

# indirect selection, v0.18.0
dbt test --select "payments" --data  
  

```