#Python/SQLAlchemy #Python/Pandas
```python
  

# for loop - read each .xlsx file in directory

for file in glob.glob('*.xlsx'):

    # print(file.lower().replace(" ",""))

    print(file)

    df = pd.read_excel(file)

    df.columns = ['col1','col2']

    df = df.iloc[5:]

    df = df.apply(lambda x: x.str.lower() if x.dtype == "object" else x)

    df['batch'] = file.lower().replace(" ","")

    df['upload_dt'] = datetime.today()

    # add column for batch date use file name lower stripped

    print(df.head())

    df.to_sql(name="table_name", schema="PIDAR", con=engine, if_exists="append", index=False)
```