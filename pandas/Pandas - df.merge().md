#Pandas #Python 
#Dataframe
# df.merge()

```python

pandas.merge(

  left, right,

  how='inner',

  on=None,

  left_on=None, right_on=None,

  left_index=False, right_index=False,

  sort=False,

  suffixes=('_x', '_y'),

  copy=None,

  indicator=False,

  validate=None)

```

ex.
```python

df1.merge(df2, how='left', on='a')

```

# df.merge() in a loop
  
Create an empty DataFrame with the columns to prevent the "key error: Code"
ex,

```python
# create empty data frame or dataframe with index

df = pd.dataframe()

for x in x_list:
    for y in y_list:
        # create dataframe result in loop
        # merge in the loop
        df = df.merge(res, on = 'x', how = 'left')
```