#Reference
#dbt 
## general config inheritance

  - #dbt prioritizes configurations in order of <b>specificity</b>, from most specificity to least specificity.
  - This generally follows the order above: an in-file config() block --> properties defined in a .yml file --> config defined in the project file.
 
## test configs inheritance

- Generic tests work a little differently when it comes to specificity. See test configs : [https://docs.getdbt.com/reference/test-configs]
  - Test configs are applied <b>hierarchically</b>:
	    1. Properties within .yml definition (generic tests only, see test properties for full syntax)
	    2. A config() block within the test's SQL definition
	    3. In dbt_project.yml

**Example**:
  - In the case of a singular test, the config() block within the SQL definition takes precedence over configs in the project file.
  - In the case of a specific instance of a generic test:
	    1. test's `.yml` properties
	    2. values set in its generic SQL definition's config()
	    3. values set in `dbt_project.yml`.

**References:**
Official Documentation : [https://docs.getdbt.com/reference/configs-and-properties#config-inheritance]