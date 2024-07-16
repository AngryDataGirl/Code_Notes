
#SQL #Python #Python/SQLAlchemy

This is the general format for the script to connect to SQL through python. 
You should have all the details to enter the host, pw, service, etc. It is the same information from the database.

```python

from sqlalchemy.engine import create_engine

DIALECT = 'oracle'
SQL_DRIVER = 'cx_oracle'
USERNAME = 'your_username' #enter your username
PASSWORD = 'your_password' #enter your password
HOST = 'subdomain.domain.tld' #enter the oracle db host url
PORT = 1521 # enter the oracle port number
SERVICE = 'your_oracle_service_name' # enter the oracle db service name

ENGINE_PATH_WIN_AUTH = DIALECT + '+' + SQL_DRIVER + '://' + USERNAME + ':' + PASSWORD +'@' + HOST + ':' + str(PORT) + '/?service_name=' + SERVICE


engine = create_engine(ENGINE_PATH_WIN_AUTH)
con = engine.connect()

#test query
import pandas as pd

test_df = pd.read_sql_query('SELECT * FROM global_name', engine)


# close connection 
con.close()
```