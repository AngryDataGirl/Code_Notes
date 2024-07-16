
#DesignPattern 
#Pandas 
#Pandas/csv

the if then block is included to handle diff columns
ie, if 4 columns, create the missing one with blank

```python
for file in glob.glob('*.xlsx'):

    print(file.lower().replace(" ",""))

    # print(file)

    df = pd.read_excel(file)

    print(len(list(df)))

    if len(list(df)) == 4:

        print("card number missing")

        df.columns = ['event_timestamp','event_message','event_location_desc','card_number']

        df['employee_name'] = np.nan

    elif len(list(df)) == 5:

        df.columns = ['event_timestamp','event_message','event_location_desc','employee_name','card_number']

    df = df.iloc[5:]

    df = df.apply(lambda x: x.str.lower() if x.dtype == "object" else x)

    df['batch'] = file.lower().replace(" ","")

    df['upload_dt'] = datetime.today()

    print(df.head())

    # add column for batch date use file name lower stripped

    print(df.columns.tolist())
```