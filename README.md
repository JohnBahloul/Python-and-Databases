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
print(df_list[0].describe())
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
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
             Population    TotalCases     NewCases    TotalDeaths   NewDeaths  \
    count  2.080000e+02  2.090000e+02     4.000000     188.000000    3.000000   
    mean   3.041549e+07  9.171850e+04  1980.500000    3792.590426  300.000000   
    std    1.047661e+08  4.325867e+05  3129.611424   15487.184877  451.199512   
    min    8.010000e+02  1.000000e+01    20.000000       1.000000    1.000000   
    25%    9.663140e+05  7.120000e+02    27.500000      22.000000   40.500000   
    50%    7.041972e+06  4.491000e+03   656.000000     113.000000   80.000000   
    75%    2.575614e+07  3.689600e+04  2609.000000     786.000000  449.500000   
    max    1.381345e+09  5.032179e+06  6590.000000  162804.000000  819.000000   
    
           TotalRecovered  NewRecovered   ActiveCases  Serious,Critical  \
    count    2.050000e+02      3.000000  2.050000e+02        122.000000   
    mean     5.887898e+04   1706.000000  2.766433e+04        534.393443   
    std      2.566984e+05   2154.779803  1.746327e+05       2047.518613   
    min      7.000000e+00     42.000000  0.000000e+00          1.000000   
    25%      3.340000e+02    489.000000  8.600000e+01          3.250000   
    50%      2.178000e+03    936.000000  8.990000e+02         27.500000   
    75%      2.055300e+04   2538.000000  7.124000e+03        160.250000   
    max      2.576668e+06   4140.000000  2.292707e+06      18296.000000   
    
           Tot Cases/1M pop  Deaths/1M pop    TotalTests   Tests/1M pop  
    count        208.000000     187.000000  1.910000e+02     191.000000  
    mean        3196.024038      98.681176  1.402405e+06   83959.366492  
    std         5191.986457     174.956862  5.553367e+06  152730.591240  
    min            3.000000       0.080000  6.100000e+01       4.000000  
    25%          282.000000       6.000000  2.575200e+04    8956.500000  
    50%         1015.000000      29.000000  1.357020e+05   32585.000000  
    75%         3841.750000      98.000000  7.576960e+05   92154.500000  
    max        39922.000000    1238.000000  6.313960e+07  995282.000000  


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

credentials = ServiceAccountCredentials.from_json_keyfile_name('/Users/johnbahloul/Desktop/Data_Projects/creds.json', scope)

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
sh.share('johnbahloul.i@gmail.com', perm_type='user', role='owner')
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
import mysql.connector
from mysql.connector.constants import ClientFlag

config = {
    'user': 'root',
    'password': 'JbahJbah_1995_1995',
    'host': '35.226.129.49',
    'client_flags': [ClientFlag.SSL],
    'ssl_ca': '/Users/johnbahloul/Desktop/Data_Projects/server-ca.pem',
    'ssl_cert': '/Users/johnbahloul/Desktop/Data_Projects/client-cert.pem',
    'ssl_key': '/Users/johnbahloul/Desktop/Data_Projects/client-key.pem'
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
import pymysql
from sqlalchemy import create_engine
engine = create_engine('mysql+pymysql://root:JbahJbah_1995_1995@35.226.129.49/coviddb', echo=False)
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
cursor.execute('show tables;')
cursor.fetchall()
```




    [('country_wise_latest',),
     ('covid_19_clean_complete',),
     ('day_wise',),
     ('full_grouped',),
     ('usa_county_wise',),
     ('worldometer_data',)]




```python
cursor.execute('describe country_wise_latest;')
pd.DataFrame(cursor.fetchall())
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Country/Region</td>
      <td>text</td>
      <td>YES</td>
      <td></td>
      <td>None</td>
      <td></td>
    </tr>
    <tr>
      <th>1</th>
      <td>Confirmed</td>
      <td>bigint(20)</td>
      <td>YES</td>
      <td></td>
      <td>None</td>
      <td></td>
    </tr>
    <tr>
      <th>2</th>
      <td>Deaths</td>
      <td>bigint(20)</td>
      <td>YES</td>
      <td></td>
      <td>None</td>
      <td></td>
    </tr>
    <tr>
      <th>3</th>
      <td>Recovered</td>
      <td>bigint(20)</td>
      <td>YES</td>
      <td></td>
      <td>None</td>
      <td></td>
    </tr>
    <tr>
      <th>4</th>
      <td>Active</td>
      <td>bigint(20)</td>
      <td>YES</td>
      <td></td>
      <td>None</td>
      <td></td>
    </tr>
    <tr>
      <th>5</th>
      <td>New cases</td>
      <td>bigint(20)</td>
      <td>YES</td>
      <td></td>
      <td>None</td>
      <td></td>
    </tr>
    <tr>
      <th>6</th>
      <td>New deaths</td>
      <td>bigint(20)</td>
      <td>YES</td>
      <td></td>
      <td>None</td>
      <td></td>
    </tr>
    <tr>
      <th>7</th>
      <td>New recovered</td>
      <td>bigint(20)</td>
      <td>YES</td>
      <td></td>
      <td>None</td>
      <td></td>
    </tr>
    <tr>
      <th>8</th>
      <td>Deaths / 100 Cases</td>
      <td>double</td>
      <td>YES</td>
      <td></td>
      <td>None</td>
      <td></td>
    </tr>
    <tr>
      <th>9</th>
      <td>Recovered / 100 Cases</td>
      <td>double</td>
      <td>YES</td>
      <td></td>
      <td>None</td>
      <td></td>
    </tr>
    <tr>
      <th>10</th>
      <td>Deaths / 100 Recovered</td>
      <td>double</td>
      <td>YES</td>
      <td></td>
      <td>None</td>
      <td></td>
    </tr>
    <tr>
      <th>11</th>
      <td>Confirmed last week</td>
      <td>bigint(20)</td>
      <td>YES</td>
      <td></td>
      <td>None</td>
      <td></td>
    </tr>
    <tr>
      <th>12</th>
      <td>1 week change</td>
      <td>bigint(20)</td>
      <td>YES</td>
      <td></td>
      <td>None</td>
      <td></td>
    </tr>
    <tr>
      <th>13</th>
      <td>1 week % increase</td>
      <td>double</td>
      <td>YES</td>
      <td></td>
      <td>None</td>
      <td></td>
    </tr>
    <tr>
      <th>14</th>
      <td>WHO Region</td>
      <td>text</td>
      <td>YES</td>
      <td></td>
      <td>None</td>
      <td></td>
    </tr>
  </tbody>
</table>
</div>




```python
cursor.execute('select * from country_wise_latest limit 10;')
pd.DataFrame(cursor.fetchall())
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
      <th>13</th>
      <th>14</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>36263</td>
      <td>1269</td>
      <td>25198</td>
      <td>9796</td>
      <td>106</td>
      <td>10</td>
      <td>18</td>
      <td>3.50</td>
      <td>69.49</td>
      <td>5.04</td>
      <td>35526</td>
      <td>737</td>
      <td>2.07</td>
      <td>Eastern Mediterranean</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Albania</td>
      <td>4880</td>
      <td>144</td>
      <td>2745</td>
      <td>1991</td>
      <td>117</td>
      <td>6</td>
      <td>63</td>
      <td>2.95</td>
      <td>56.25</td>
      <td>5.25</td>
      <td>4171</td>
      <td>709</td>
      <td>17.00</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Algeria</td>
      <td>27973</td>
      <td>1163</td>
      <td>18837</td>
      <td>7973</td>
      <td>616</td>
      <td>8</td>
      <td>749</td>
      <td>4.16</td>
      <td>67.34</td>
      <td>6.17</td>
      <td>23691</td>
      <td>4282</td>
      <td>18.07</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andorra</td>
      <td>907</td>
      <td>52</td>
      <td>803</td>
      <td>52</td>
      <td>10</td>
      <td>0</td>
      <td>0</td>
      <td>5.73</td>
      <td>88.53</td>
      <td>6.48</td>
      <td>884</td>
      <td>23</td>
      <td>2.60</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Angola</td>
      <td>950</td>
      <td>41</td>
      <td>242</td>
      <td>667</td>
      <td>18</td>
      <td>1</td>
      <td>0</td>
      <td>4.32</td>
      <td>25.47</td>
      <td>16.94</td>
      <td>749</td>
      <td>201</td>
      <td>26.84</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Antigua and Barbuda</td>
      <td>86</td>
      <td>3</td>
      <td>65</td>
      <td>18</td>
      <td>4</td>
      <td>0</td>
      <td>5</td>
      <td>3.49</td>
      <td>75.58</td>
      <td>4.62</td>
      <td>76</td>
      <td>10</td>
      <td>13.16</td>
      <td>Americas</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Argentina</td>
      <td>167416</td>
      <td>3059</td>
      <td>72575</td>
      <td>91782</td>
      <td>4890</td>
      <td>120</td>
      <td>2057</td>
      <td>1.83</td>
      <td>43.35</td>
      <td>4.21</td>
      <td>130774</td>
      <td>36642</td>
      <td>28.02</td>
      <td>Americas</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Armenia</td>
      <td>37390</td>
      <td>711</td>
      <td>26665</td>
      <td>10014</td>
      <td>73</td>
      <td>6</td>
      <td>187</td>
      <td>1.90</td>
      <td>71.32</td>
      <td>2.67</td>
      <td>34981</td>
      <td>2409</td>
      <td>6.89</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Australia</td>
      <td>15303</td>
      <td>167</td>
      <td>9311</td>
      <td>5825</td>
      <td>368</td>
      <td>6</td>
      <td>137</td>
      <td>1.09</td>
      <td>60.84</td>
      <td>1.79</td>
      <td>12428</td>
      <td>2875</td>
      <td>23.13</td>
      <td>Western Pacific</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Austria</td>
      <td>20558</td>
      <td>713</td>
      <td>18246</td>
      <td>1599</td>
      <td>86</td>
      <td>1</td>
      <td>37</td>
      <td>3.47</td>
      <td>88.75</td>
      <td>3.91</td>
      <td>19743</td>
      <td>815</td>
      <td>4.13</td>
      <td>Europe</td>
    </tr>
  </tbody>
</table>
</div>
