# Python-and-Databases
Leverage Python and other open sources tools to create and manage databases


# Import and Process Data
---

[Kaggle Dataset](https://www.kaggle.com/imdevskp/corona-virus-report?select=country_wise_latest.csv)

The following code aims to import and preview all csv files 


```python
import pandas as pd
import os
import glob
import numpy as np

pd.set_option('display.max_rows', 50000)
pd.set_option('display.max_columns', 50000)

# use glob to get all the csv files in the folder
path = "path to folder"
csv_files = glob.glob(os.path.join(path, "*.csv"))

# loop over the list of csv files
df_list_name = []
df_list = []

for f in csv_files:
    # read the csv file
    df = pd.read_csv(f)
    # removal of infinity data points will allow for the MySQL DB to be populated with pandas dataframes
    df = df.replace([np.inf, -np.inf], np.nan)    
    # add new dfs to list
    df_list.append(df)
    df_list_name.append(f[47:-4])
    
# Preview First Data Frame
display(df_list[0].head())
print(df_list[0].info())
```


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country/Region</th>
      <th>Continent</th>
      <th>Population</th>
      <th>TotalCases</th>
      <th>NewCases</th>
      <th>TotalDeaths</th>
      <th>NewDeaths</th>
      <th>TotalRecovered</th>
      <th>NewRecovered</th>
      <th>ActiveCases</th>
      <th>Serious,Critical</th>
      <th>Tot Cases/1M pop</th>
      <th>Deaths/1M pop</th>
      <th>TotalTests</th>
      <th>Tests/1M pop</th>
      <th>WHO Region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>USA</td>
      <td>North America</td>
      <td>3.311981e+08</td>
      <td>5032179</td>
      <td>NaN</td>
      <td>162804.0</td>
      <td>NaN</td>
      <td>2576668.0</td>
      <td>NaN</td>
      <td>2292707.0</td>
      <td>18296.0</td>
      <td>15194.0</td>
      <td>492.0</td>
      <td>63139605.0</td>
      <td>190640.0</td>
      <td>Americas</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Brazil</td>
      <td>South America</td>
      <td>2.127107e+08</td>
      <td>2917562</td>
      <td>NaN</td>
      <td>98644.0</td>
      <td>NaN</td>
      <td>2047660.0</td>
      <td>NaN</td>
      <td>771258.0</td>
      <td>8318.0</td>
      <td>13716.0</td>
      <td>464.0</td>
      <td>13206188.0</td>
      <td>62085.0</td>
      <td>Americas</td>
    </tr>
    <tr>
      <th>2</th>
      <td>India</td>
      <td>Asia</td>
      <td>1.381345e+09</td>
      <td>2025409</td>
      <td>NaN</td>
      <td>41638.0</td>
      <td>NaN</td>
      <td>1377384.0</td>
      <td>NaN</td>
      <td>606387.0</td>
      <td>8944.0</td>
      <td>1466.0</td>
      <td>30.0</td>
      <td>22149351.0</td>
      <td>16035.0</td>
      <td>South-EastAsia</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Russia</td>
      <td>Europe</td>
      <td>1.459409e+08</td>
      <td>871894</td>
      <td>NaN</td>
      <td>14606.0</td>
      <td>NaN</td>
      <td>676357.0</td>
      <td>NaN</td>
      <td>180931.0</td>
      <td>2300.0</td>
      <td>5974.0</td>
      <td>100.0</td>
      <td>29716907.0</td>
      <td>203623.0</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>4</th>
      <td>South Africa</td>
      <td>Africa</td>
      <td>5.938157e+07</td>
      <td>538184</td>
      <td>NaN</td>
      <td>9604.0</td>
      <td>NaN</td>
      <td>387316.0</td>
      <td>NaN</td>
      <td>141264.0</td>
      <td>539.0</td>
      <td>9063.0</td>
      <td>162.0</td>
      <td>3149807.0</td>
      <td>53044.0</td>
      <td>Africa</td>
    </tr>
  </tbody>
</table>
</div>


    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 209 entries, 0 to 208
    Data columns (total 16 columns):
     #   Column            Non-Null Count  Dtype  
    ---  ------            --------------  -----  
     0   Country/Region    209 non-null    object 
     1   Continent         208 non-null    object 
     2   Population        208 non-null    float64
     3   TotalCases        209 non-null    int64  
     4   NewCases          4 non-null      float64
     5   TotalDeaths       188 non-null    float64
     6   NewDeaths         3 non-null      float64
     7   TotalRecovered    205 non-null    float64
     8   NewRecovered      3 non-null      float64
     9   ActiveCases       205 non-null    float64
     10  Serious,Critical  122 non-null    float64
     11  Tot Cases/1M pop  208 non-null    float64
     12  Deaths/1M pop     187 non-null    float64
     13  TotalTests        191 non-null    float64
     14  Tests/1M pop      191 non-null    float64
     15  WHO Region        184 non-null    object 
    dtypes: float64(12), int64(1), object(3)
    memory usage: 26.2+ KB
    None


# Create Googlesheet Database
---
[Google Sheets API Setup](youtube.com/watch?v=larTWACNYjo)

[Gspread Docs](https://docs.gspread.org/en/latest/user-guide.html#creating-a-spreadsheethttps://docs.gspread.org/en/latest/user-guide.html#creating-a-spreadsheet)

[Gspread-dataframe Docs](https://pypi.org/project/gspread-dataframe/https://pypi.org/project/gspread-dataframe/)


```python
import gspread
import gspread_dataframe as gd
from oauth2client.service_account import ServiceAccountCredentials

# Authorize credentials
scope = ["https://spreadsheets.google.com/feeds",
         'https://www.googleapis.com/auth/spreadsheets',
         "https://www.googleapis.com/auth/drive.file",
         "https://www.googleapis.com/auth/drive"]

credentials = ServiceAccountCredentials.from_json_keyfile_name('creds.json', scope)

client = gspread.authorize(credentials)
```


```python
# Create Googlesheet DB
try:
    # Creates the googlesheet
    coviddb = client.create('CovidDatabase')
    print('DB Created Successfully')
    print(f'Database ID: {coviddb}')
except Exception as e:
    print(e)    
```

    DB Created Successfully
    Database ID: <Spreadsheet 'CovidDatabase' id:1AbuZdm5pfzMQRC6EQYaX7d5Kk-uWT_VRppiSPsGTzlc>



```python
# Open spreadsheet to enable editing
sh = client.open('CovidDatabase')

# Share spreadsheet
sh.share('email', perm_type='user', role='owner')
```


```python
# Add csv generated dataframes while creating individual worksheets
for i, n in zip(df_list, df_list_name):
    try:
        # Create a worksheet
        sheet = sh.add_worksheet(title=str(n), rows = len(df_list[0].columns), cols = len(df_list[0].index))
        print(f'Worksheet {str(n)} created successfully')
        
        # Open to newly created worsheet
        client.open("CovidDatabase").worksheet(str(n))
        
        # Add dataframe to Covid DB
        gd.set_with_dataframe(sheet,i)
        print(f'Dataframe {str(n)} added successfully')
        print('--------------------------------------')
    except Exception as e:
        print(e)
        pass
```

    Worksheet worldometer_data created successfully
    Dataframe worldometer_data added successfully
    --------------------------------------
    Worksheet full_grouped created successfully
    Dataframe full_grouped added successfully
    --------------------------------------
    Worksheet day_wise created successfully
    Dataframe day_wise added successfully
    --------------------------------------
    Worksheet covid_19_clean_complete created successfully
    Dataframe covid_19_clean_complete added successfully
    --------------------------------------
    Worksheet country_wise_latest created successfully
    Dataframe country_wise_latest added successfully
    --------------------------------------
    Worksheet usa_county_wise created successfully
    ('Connection aborted.', timeout('The write operation timed out'))


# Create Google Cloud SQL Database
---

[SQL on The Cloud With Python](https://towardsdatascience.com/sql-on-the-cloud-with-python-c08a30807661)

The MySQL Database is created using the Google Cloud Console.


```python
# Connect to the database over a protected Network
import mysql.connector
from mysql.connector.constants import ClientFlag

config = {
    'user': 'root',
    'password': '',
    'host': '',
    'client_flags': [ClientFlag.SSL],
    'ssl_ca': '',
    'ssl_cert': '',
    'ssl_key': ''
}
```


```python
# now we establish our connection
try:
    # Creates the googlesheet
    conn = mysql.connector.connect(**config)
    print('Successfully connected to google cloud instance')
    # initialize connection cursor
    cursor = conn.cursor()
    print('Connection curser initialized')
except Exception as e:
    print(e)    
```

    Successfully connected to google cloud instance
    Connection curser initialized



```python
# create a 'coviddb' database
cursor.execute('CREATE DATABASE coviddb')
```


```python
# add csv files as tables to the google cloud MySQL DB
import pymysql
from sqlalchemy import create_engine
engine = create_engine('')
engine.connect()

# Create 
for i,n in zip(df_list,df_list_name):
    try:
        i.to_sql(str(n),con = engine, if_exists='replace', index=False)
        print(f'Table {str(n)} created and added to MySQL DB successfully')
        print('--------------------------------------')
    except Exception as e:
        print(e)
        pass
```

    Table worldometer_data created and added to MySQL DB successfully
    --------------------------------------
    Table full_grouped created and added to MySQL DB successfully
    --------------------------------------
    Table day_wise created and added to MySQL DB successfully
    --------------------------------------
    Table covid_19_clean_complete created and added to MySQL DB successfully
    --------------------------------------
    Table country_wise_latest created and added to MySQL DB successfully
    --------------------------------------
    Table usa_county_wise created and added to MySQL DB successfully
    --------------------------------------



```python
# confirm the data was added to the DB successfully
cursor.execute('USE coviddb')
```


```python
from sqlalchemy.orm import Query
from sqlalchemy.engine import reflection
from sqlalchemy import inspect
import sqlalchemy as db
import warnings
warnings.filterwarnings('ignore')
```


```python
insp = reflection.Inspector.from_engine(engine)
```


```python
insp.get_schema_names()
```




    ['information_schema', 'coviddb', 'mysql', 'performance_schema', 'sys']




```python
tables = insp.get_table_names(schema = 'coviddb')
tables
```




    ['country_wise_latest',
     'covid_19_clean_complete',
     'day_wise',
     'full_grouped',
     'usa_county_wise',
     'worldometer_data']




```python
# Get column information
columns = insp.get_columns(table_name='worldometer_data',schema = 'coviddb')
pd.DataFrame(columns)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>type</th>
      <th>default</th>
      <th>comment</th>
      <th>nullable</th>
      <th>autoincrement</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Country/Region</td>
      <td>TEXT</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Continent</td>
      <td>TEXT</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Population</td>
      <td>DOUBLE</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>TotalCases</td>
      <td>BIGINT</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NewCases</td>
      <td>DOUBLE</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>TotalDeaths</td>
      <td>DOUBLE</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NewDeaths</td>
      <td>DOUBLE</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>TotalRecovered</td>
      <td>DOUBLE</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NewRecovered</td>
      <td>DOUBLE</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>ActiveCases</td>
      <td>DOUBLE</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Serious,Critical</td>
      <td>DOUBLE</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Tot Cases/1M pop</td>
      <td>DOUBLE</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Deaths/1M pop</td>
      <td>DOUBLE</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>13</th>
      <td>TotalTests</td>
      <td>DOUBLE</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Tests/1M pop</td>
      <td>DOUBLE</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15</th>
      <td>WHO Region</td>
      <td>TEXT</td>
      <td>None</td>
      <td>None</td>
      <td>True</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
connection = engine.connect()
metadata = db.MetaData(schema='coviddb')

# Define the Tables you want to Query
worldometer_data = db.Table('worldometer_data', metadata, autoload=True, autoload_with=engine)
```


```python
#Equivalent to 'SELECT * ...'
query = db.select([worldometer_data]).limit(10)

ResultProxy = connection.execute(query)
ResultSet = ResultProxy.fetchall()

# Create pandas dataframe
df = pd.DataFrame(ResultSet)
df.columns = ResultSet[0].keys()
```


```python
df
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country/Region</th>
      <th>Continent</th>
      <th>Population</th>
      <th>TotalCases</th>
      <th>NewCases</th>
      <th>TotalDeaths</th>
      <th>NewDeaths</th>
      <th>TotalRecovered</th>
      <th>NewRecovered</th>
      <th>ActiveCases</th>
      <th>Serious,Critical</th>
      <th>Tot Cases/1M pop</th>
      <th>Deaths/1M pop</th>
      <th>TotalTests</th>
      <th>Tests/1M pop</th>
      <th>WHO Region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>USA</td>
      <td>North America</td>
      <td>331198130.0000000000</td>
      <td>5032179</td>
      <td>None</td>
      <td>162804.0000000000</td>
      <td>None</td>
      <td>2576668.0000000000</td>
      <td>None</td>
      <td>2292707.0000000000</td>
      <td>18296.0000000000</td>
      <td>15194.0000000000</td>
      <td>492.0000000000</td>
      <td>63139605.0000000000</td>
      <td>190640.0000000000</td>
      <td>Americas</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Brazil</td>
      <td>South America</td>
      <td>212710692.0000000000</td>
      <td>2917562</td>
      <td>None</td>
      <td>98644.0000000000</td>
      <td>None</td>
      <td>2047660.0000000000</td>
      <td>None</td>
      <td>771258.0000000000</td>
      <td>8318.0000000000</td>
      <td>13716.0000000000</td>
      <td>464.0000000000</td>
      <td>13206188.0000000000</td>
      <td>62085.0000000000</td>
      <td>Americas</td>
    </tr>
    <tr>
      <th>2</th>
      <td>India</td>
      <td>Asia</td>
      <td>1381344997.0000000000</td>
      <td>2025409</td>
      <td>None</td>
      <td>41638.0000000000</td>
      <td>None</td>
      <td>1377384.0000000000</td>
      <td>None</td>
      <td>606387.0000000000</td>
      <td>8944.0000000000</td>
      <td>1466.0000000000</td>
      <td>30.0000000000</td>
      <td>22149351.0000000000</td>
      <td>16035.0000000000</td>
      <td>South-EastAsia</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Russia</td>
      <td>Europe</td>
      <td>145940924.0000000000</td>
      <td>871894</td>
      <td>None</td>
      <td>14606.0000000000</td>
      <td>None</td>
      <td>676357.0000000000</td>
      <td>None</td>
      <td>180931.0000000000</td>
      <td>2300.0000000000</td>
      <td>5974.0000000000</td>
      <td>100.0000000000</td>
      <td>29716907.0000000000</td>
      <td>203623.0000000000</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>4</th>
      <td>South Africa</td>
      <td>Africa</td>
      <td>59381566.0000000000</td>
      <td>538184</td>
      <td>None</td>
      <td>9604.0000000000</td>
      <td>None</td>
      <td>387316.0000000000</td>
      <td>None</td>
      <td>141264.0000000000</td>
      <td>539.0000000000</td>
      <td>9063.0000000000</td>
      <td>162.0000000000</td>
      <td>3149807.0000000000</td>
      <td>53044.0000000000</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Mexico</td>
      <td>North America</td>
      <td>129066160.0000000000</td>
      <td>462690</td>
      <td>6590.0000000000</td>
      <td>50517.0000000000</td>
      <td>819.0000000000</td>
      <td>308848.0000000000</td>
      <td>4140.0000000000</td>
      <td>103325.0000000000</td>
      <td>3987.0000000000</td>
      <td>3585.0000000000</td>
      <td>391.0000000000</td>
      <td>1056915.0000000000</td>
      <td>8189.0000000000</td>
      <td>Americas</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Peru</td>
      <td>South America</td>
      <td>33016319.0000000000</td>
      <td>455409</td>
      <td>None</td>
      <td>20424.0000000000</td>
      <td>None</td>
      <td>310337.0000000000</td>
      <td>None</td>
      <td>124648.0000000000</td>
      <td>1426.0000000000</td>
      <td>13793.0000000000</td>
      <td>619.0000000000</td>
      <td>2493429.0000000000</td>
      <td>75521.0000000000</td>
      <td>Americas</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Chile</td>
      <td>South America</td>
      <td>19132514.0000000000</td>
      <td>366671</td>
      <td>None</td>
      <td>9889.0000000000</td>
      <td>None</td>
      <td>340168.0000000000</td>
      <td>None</td>
      <td>16614.0000000000</td>
      <td>1358.0000000000</td>
      <td>19165.0000000000</td>
      <td>517.0000000000</td>
      <td>1760615.0000000000</td>
      <td>92022.0000000000</td>
      <td>Americas</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Colombia</td>
      <td>South America</td>
      <td>50936262.0000000000</td>
      <td>357710</td>
      <td>None</td>
      <td>11939.0000000000</td>
      <td>None</td>
      <td>192355.0000000000</td>
      <td>None</td>
      <td>153416.0000000000</td>
      <td>1493.0000000000</td>
      <td>7023.0000000000</td>
      <td>234.0000000000</td>
      <td>1801835.0000000000</td>
      <td>35374.0000000000</td>
      <td>Americas</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Spain</td>
      <td>Europe</td>
      <td>46756648.0000000000</td>
      <td>354530</td>
      <td>None</td>
      <td>28500.0000000000</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>617.0000000000</td>
      <td>7582.0000000000</td>
      <td>610.0000000000</td>
      <td>7064329.0000000000</td>
      <td>151087.0000000000</td>
      <td>Europe</td>
    </tr>
  </tbody>
</table>
</div>
