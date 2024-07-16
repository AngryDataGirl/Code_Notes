#Pandas #Dataframe


```python

all_res = []

for df in df_all:

    for i in substr:

        res = df[df['url'].str.contains(i)]

        all_res.append(res)

  

df_res = pd.concat(all_res)

```
