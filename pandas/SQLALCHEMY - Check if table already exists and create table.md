```Python
  

### TABLE CREATION ###

# checks if the table already exists or not CREATE IF NOT EXISTS

if sql.inspect(engine).has_table("carte_acces") == False:

    print("THIS TABLE DOES NOT EXIST.")

    # create table with primary key - one time operation

    metadata_obj = sql.MetaData()

    # database name

    TABLE_NAME = sql.Table(
        'TABLE_NAME',                                        
        metadata_obj,                                    

        sql.Column('COL1', sql.String(500)),  
        sql.Column('COL2', sql.String(2000)),                    
        sql.Column('COL3', sql.String(2000)),                
        sql.Column('COL4', sql.String(1000)),
        sql.Column('COL5', sql.String(1000)),
        sql.Column('COL6', sql.Date),
    )

    # Create the profile table

    metadata_obj.create_all(engine)

    # print(metadata_obj.create_all(engine)

    print("TABLE CREATED.")

else:

    print("TABLE EXISTS.")

### TABLE CREATION END ###

```