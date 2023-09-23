# sqlite_database_operations

# Datasets Explored

I decided to use datasets about standard charges from Saint Joseph's Hospital and Maimondies Medical Center. The dataset from Saint Joseph's Hospital contained columns for billing / charge code, charge description, Rev Code, CPT / HCPC, price, NDC, package size, package unit, package description and charge quantity. This dataset contained columns with int, float, real, and string. The dataset from Maimonides Medical Center contains columns for CDM, CDM description, and charge amount. This dataset contains columns with float and string. However, I'm not too sure what datatype would be applicable for the CDM column. 

# EDA Analysis

Prior to doing any calculations, I cleaned up the column names and addressed missing values that both datasets may have had. The dataset from Saint Joseph's Hospital had thousands of missing values in the CPT / HCPC, price, NDC, package size, package unit, package description, and charge quantity columns. On the other hand, the dataset from Maimonides Medical Center had no missing values in any of its columns. 

For the calculations, I found the mean, median, mode, range, variance, standard deviation, and interquartile range (IQR) values for the numerical columns that were not "secretly" categorical of both datasets. For the dataset from Saint Joseph's Hospital, I did these calculations on the price and package size columns. For the dataset from Maimonides Medical Center, I only did these calculations on the charge amount column. Following these calculations, histograms were made for all of the columns that the calculations were done on. For all of the values in columns that were categorical, value counts were done on them to determine the frequency of each data.

# Replicating SQLite Set Up 

1. Import create_engine and sqlite3
  - ``` from sqlalchemy import create_engine```
  - ``` import sqlite3```
   
2. Connect sqlite3 to a database you want to create.
  - ``` conn = sqlite3.connect('health.db')```
  - ```c = conn.cursor()```
   
3. Create the table with the name of the column and what data type is to be associated with each column

```
c.execute('''
CREATE TABLE IF NOT EXISTS chs
(
[chargedescription], text
[revcode] int,
[price] float,
[packagesize] float,
[packagedescription] text
)
''')
conn.commit()
``` 
4. Insert the values into the table.
```
c.execute('''
INSERT INTO chs
VALUES
('COVID-Vaccine', 927, 100.00, 100.00, 'Vaccine'),
('Aspirin', 329, 45.00, 100.00, 'Pill')
''')
```

5. Commit the changes
``` conn.commit()```

6. Ensure that the name of the table is what was initially created.

```
c.execute('''
SELECT name
FROM sqlite_master
WHERE type = 'table'
''')

data = c.fetchall()
for values in data:
print(value)

```

7. Ensure that the values added are included in the table.

```
c.execute('''
SELECT * FROM chs;
''')
print(c.fetchall())
```

8. Connect the table created to a SQL database using an engine.

```
engine = create_engine('sqlite:///health.db')
```

9. Display the values created.

```
chs = pd.read_sql("select * from chs;", conn)
chs
```

10. Close the connection.

-```chs.to_sql('chs', conn, if if_exists = 'replace', index=False)```
-```conn.close()```
