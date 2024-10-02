```python
import os
import pandas as pd
import m1_config as impc

# Print confirmation

os.chdir(impc.save_directory)  

print("Reading files in: ",impc.save_directory)

  

# Get a list of all csv files in the current directory

csv_files = [f for f in os.listdir(os.curdir) if f.endswith('.csv')]

  

# Create a Pandas Excel writer using XlsxWriter as the engine

writer = pd.ExcelWriter(impc.combined_filename+'.xlsx', engine='xlsxwriter')

  

# Loop through the list of csv files

for csv in csv_files:

    df = pd.read_csv(csv)  # Read each csv file into a DataFrame

    print("Saving csv:",csv,"to tab")

    df.to_excel(writer, sheet_name=os.path.splitext(csv)[0], index=False)  # Write DataFrame to an excel sheet

  

# Close the Pandas Excel writer and output the Excel file

writer.close()
```
