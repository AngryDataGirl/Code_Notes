# Setting up tests for your dbt project 

https://docs.getdbt.com/docs/build/data-tests#:~:text=When%20you%20run%20dbt%20test,%20dbt%20will%20tell%20you%20if

The simplest way to define a data test is by writing the exact SQL that will return failing records. We call these "singular" data tests, because they're one-off assertions usable for a single purpose.

These tests are defined in .sql files, typically in your tests directory (as defined by your test-paths config). You can use Jinja (including ref and source) in the test definition, just like you can when creating models. Each .sql file contains one select statement, and it defines one data test.

## Where to save singular tests

save singular #dbtTests  as sql queries in the test path, no need to put them in directory, #dbt will know where to find them so long as they are with your other tests  

## Defining custom test names

[define a custom name for one test](https://docs.getdbt.com/reference/resource-properties/tests#define-a-custom-name-for-one-test)

By default, #dbt will synthesize a name for your generic test by concatenating:

- test name (not_null, unique, etc)
- model name (or source/seed/snapshot)
- column name (if relevant)
- arguments (if relevant, e.g. values for accepted_values)

It does not include any configurations for the test. If the concatenated name is too long, dbt will use a truncated and hashed version instead. The goal is to preserve unique identifiers for all resources in your project, including tests.

> [!Tip] 
> It helps to name the test after the "failure case", ie, this means that the test name is the reason the record exists

By defining a custom name, you get full control over how the test will appear in log messages and metadata artifacts. You'll also be able to select the test by that name.

```yaml

version: 2

models:
  - name: orders
    columns:
      - name: status
        tests:
          - accepted_values:
              name: unexpected_order_status_today
              values: ['placed', 'shipped', 'completed', 'returned']
              config:
                severity: warn
                warn_if: ">0"
              custom_operator: '<'
			  supplied_values: (99)

```
