#Pandas #Python #Columns
# selecting multiple columns

```python
df1 = df[['a', 'b']]
```

# selecting multiple columns through slice

```python

# Remember, Python is zero-offset! The "third" entry is at slot two.
newdf = df[df.columns[2:4]]
  
# or !
columns = ['b', 'c']
df1 = pd.DataFrame(df, columns=columns)

```

