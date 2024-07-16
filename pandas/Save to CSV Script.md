#Python #Python/SQLAlchemy #M1 #M2
```python
### IMPORTS ###

import os

import pandas as pd

import sqlalchemy as sql

import glob

import numpy as np

from datetime import datetime

  

### config to import

import m1_config as impc

  

# CREATE CONNECTION

engine = sql.create_engine(impc.DIALECT + '+' + impc.SQL_DRIVER + '://' + impc.USERNAME + ':' + impc.PASSWORD +'@' + impc.HOST + ':' + str(impc.PORT) + '/?service_name=' + impc.SERVICE)

con = engine.connect()

  

print("Successfully connected to:", impc.HOST, "with", impc.USERNAME)

  

### QUERIES ###

# print(impc.queries.keys())

# print(impc.queries.values())

  

### Enter wd where you want to save queries ###

os.chdir(impc.save_directory)  

print("files will be saved in", impc.save_directory)

  

for query_name, query in impc.queries.items():

    df = pd.read_sql_query(query, engine)

    print("SAVING",query_name)

    file_name = impc.save_directory+query_name+'.csv'

    df.to_csv(file_name, index=False)

    print("QUERY SAVED.")

  

# close connection

con.close()
```