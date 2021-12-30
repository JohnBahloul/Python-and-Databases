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
path = "/Users/johnbahloul/Downloads/covid_data_kaggle/"
csv_files = glob.glob(os.path.join(path, "*.csv"))

# loop over the list of csv files
df_list_name = []
df_list = []

for f in csv_files:
    # read the csv file
    df = pd.read_csv(f)
    # removal of infinity data points will allow for the MySQL DB to be populated with pandas dataframes
    df = df.replace([np.inf, -np.inf], np.nan)
    
    # print the location and filename
    print('Location:', f)
    print('File Name:', f[47:-4])
    
    # print content and preview csv file dfs
    print('Content:')
    print(len(df))
    display(df.head())
    print(df.info())
    print(df.describe())
    
    # add new dfs to list
    df_list.append(df)
    df_list_name.append(f[47:-4])
```

    Location: /Users/johnbahloul/Downloads/covid_data_kaggle/worldometer_data.csv
    File Name: worldometer_data
    Content:
    209



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
    Location: /Users/johnbahloul/Downloads/covid_data_kaggle/full_grouped.csv
    File Name: full_grouped
    Content:
    35156



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
      <th>Date</th>
      <th>Country/Region</th>
      <th>Confirmed</th>
      <th>Deaths</th>
      <th>Recovered</th>
      <th>Active</th>
      <th>New cases</th>
      <th>New deaths</th>
      <th>New recovered</th>
      <th>WHO Region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-01-22</td>
      <td>Afghanistan</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Eastern Mediterranean</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-22</td>
      <td>Albania</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-01-22</td>
      <td>Algeria</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-01-22</td>
      <td>Andorra</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-01-22</td>
      <td>Angola</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Africa</td>
    </tr>
  </tbody>
</table>
</div>


    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 35156 entries, 0 to 35155
    Data columns (total 10 columns):
     #   Column          Non-Null Count  Dtype 
    ---  ------          --------------  ----- 
     0   Date            35156 non-null  object
     1   Country/Region  35156 non-null  object
     2   Confirmed       35156 non-null  int64 
     3   Deaths          35156 non-null  int64 
     4   Recovered       35156 non-null  int64 
     5   Active          35156 non-null  int64 
     6   New cases       35156 non-null  int64 
     7   New deaths      35156 non-null  int64 
     8   New recovered   35156 non-null  int64 
     9   WHO Region      35156 non-null  object
    dtypes: int64(7), object(3)
    memory usage: 2.7+ MB
    None
              Confirmed         Deaths     Recovered        Active    New cases  \
    count  3.515600e+04   35156.000000  3.515600e+04  3.515600e+04  35156.00000   
    mean   2.356663e+04    1234.068239  1.104813e+04  1.128443e+04    469.36375   
    std    1.499818e+05    7437.238354  6.454640e+04  8.997149e+04   3005.86754   
    min    0.000000e+00       0.000000  0.000000e+00 -2.000000e+00      0.00000   
    25%    1.000000e+00       0.000000  0.000000e+00  0.000000e+00      0.00000   
    50%    2.500000e+02       4.000000  3.300000e+01  8.500000e+01      2.00000   
    75%    3.640250e+03      78.250000  1.286250e+03  1.454000e+03     75.00000   
    max    4.290259e+06  148011.000000  1.846641e+06  2.816444e+06  77255.00000   
    
             New deaths  New recovered  
    count  35156.000000   35156.000000  
    mean      18.603339     269.315593  
    std      115.706351    2068.063852  
    min    -1918.000000  -16298.000000  
    25%        0.000000       0.000000  
    50%        0.000000       0.000000  
    75%        1.000000      20.000000  
    max     3887.000000  140050.000000  
    Location: /Users/johnbahloul/Downloads/covid_data_kaggle/day_wise.csv
    File Name: day_wise
    Content:
    188



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
      <th>Date</th>
      <th>Confirmed</th>
      <th>Deaths</th>
      <th>Recovered</th>
      <th>Active</th>
      <th>New cases</th>
      <th>New deaths</th>
      <th>New recovered</th>
      <th>Deaths / 100 Cases</th>
      <th>Recovered / 100 Cases</th>
      <th>Deaths / 100 Recovered</th>
      <th>No. of countries</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-01-22</td>
      <td>555</td>
      <td>17</td>
      <td>28</td>
      <td>510</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3.06</td>
      <td>5.05</td>
      <td>60.71</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-23</td>
      <td>654</td>
      <td>18</td>
      <td>30</td>
      <td>606</td>
      <td>99</td>
      <td>1</td>
      <td>2</td>
      <td>2.75</td>
      <td>4.59</td>
      <td>60.00</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-01-24</td>
      <td>941</td>
      <td>26</td>
      <td>36</td>
      <td>879</td>
      <td>287</td>
      <td>8</td>
      <td>6</td>
      <td>2.76</td>
      <td>3.83</td>
      <td>72.22</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-01-25</td>
      <td>1434</td>
      <td>42</td>
      <td>39</td>
      <td>1353</td>
      <td>493</td>
      <td>16</td>
      <td>3</td>
      <td>2.93</td>
      <td>2.72</td>
      <td>107.69</td>
      <td>11</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-01-26</td>
      <td>2118</td>
      <td>56</td>
      <td>52</td>
      <td>2010</td>
      <td>684</td>
      <td>14</td>
      <td>13</td>
      <td>2.64</td>
      <td>2.46</td>
      <td>107.69</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>


    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 188 entries, 0 to 187
    Data columns (total 12 columns):
     #   Column                  Non-Null Count  Dtype  
    ---  ------                  --------------  -----  
     0   Date                    188 non-null    object 
     1   Confirmed               188 non-null    int64  
     2   Deaths                  188 non-null    int64  
     3   Recovered               188 non-null    int64  
     4   Active                  188 non-null    int64  
     5   New cases               188 non-null    int64  
     6   New deaths              188 non-null    int64  
     7   New recovered           188 non-null    int64  
     8   Deaths / 100 Cases      188 non-null    float64
     9   Recovered / 100 Cases   188 non-null    float64
     10  Deaths / 100 Recovered  188 non-null    float64
     11  No. of countries        188 non-null    int64  
    dtypes: float64(3), int64(8), object(1)
    memory usage: 17.8+ KB
    None
              Confirmed         Deaths     Recovered        Active      New cases  \
    count  1.880000e+02     188.000000  1.880000e+02  1.880000e+02     188.000000   
    mean   4.406960e+06  230770.760638  2.066001e+06  2.110188e+06   87771.021277   
    std    4.757988e+06  217929.094183  2.627976e+06  1.969670e+06   75295.293255   
    min    5.550000e+02      17.000000  2.800000e+01  5.100000e+02       0.000000   
    25%    1.121910e+05    3935.000000  6.044125e+04  5.864175e+04    5568.500000   
    50%    2.848733e+06  204190.000000  7.847840e+05  1.859759e+06   81114.000000   
    75%    7.422046e+06  418634.500000  3.416396e+06  3.587015e+06  131502.500000   
    max    1.648048e+07  654036.000000  9.468087e+06  6.358362e+06  282756.000000   
    
            New deaths  New recovered  Deaths / 100 Cases  Recovered / 100 Cases  \
    count   188.000000     188.000000          188.000000             188.000000   
    mean   3478.824468   50362.015957            4.860638              34.343936   
    std    2537.735652   56090.892479            1.579541              16.206159   
    min       0.000000       0.000000            2.040000               1.710000   
    25%     250.750000    2488.250000            3.510000              22.785000   
    50%    4116.000000   30991.500000            4.850000              35.680000   
    75%    5346.000000   79706.250000            6.297500              48.945000   
    max    9966.000000  284394.000000            7.180000              57.450000   
    
           Deaths / 100 Recovered  No. of countries  
    count              188.000000        188.000000  
    mean                22.104521        144.351064  
    std                 22.568307         65.175979  
    min                  6.260000          6.000000  
    25%                  9.650000        101.250000  
    50%                 15.380000        184.000000  
    75%                 25.342500        187.000000  
    max                134.430000        187.000000  
    Location: /Users/johnbahloul/Downloads/covid_data_kaggle/covid_19_clean_complete.csv
    File Name: covid_19_clean_complete
    Content:
    49068



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
      <th>Province/State</th>
      <th>Country/Region</th>
      <th>Lat</th>
      <th>Long</th>
      <th>Date</th>
      <th>Confirmed</th>
      <th>Deaths</th>
      <th>Recovered</th>
      <th>Active</th>
      <th>WHO Region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>Afghanistan</td>
      <td>33.93911</td>
      <td>67.709953</td>
      <td>2020-01-22</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Eastern Mediterranean</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>Albania</td>
      <td>41.15330</td>
      <td>20.168300</td>
      <td>2020-01-22</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>Algeria</td>
      <td>28.03390</td>
      <td>1.659600</td>
      <td>2020-01-22</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>Andorra</td>
      <td>42.50630</td>
      <td>1.521800</td>
      <td>2020-01-22</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>Angola</td>
      <td>-11.20270</td>
      <td>17.873900</td>
      <td>2020-01-22</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Africa</td>
    </tr>
  </tbody>
</table>
</div>


    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 49068 entries, 0 to 49067
    Data columns (total 10 columns):
     #   Column          Non-Null Count  Dtype  
    ---  ------          --------------  -----  
     0   Province/State  14664 non-null  object 
     1   Country/Region  49068 non-null  object 
     2   Lat             49068 non-null  float64
     3   Long            49068 non-null  float64
     4   Date            49068 non-null  object 
     5   Confirmed       49068 non-null  int64  
     6   Deaths          49068 non-null  int64  
     7   Recovered       49068 non-null  int64  
     8   Active          49068 non-null  int64  
     9   WHO Region      49068 non-null  object 
    dtypes: float64(2), int64(4), object(4)
    memory usage: 3.7+ MB
    None
                    Lat          Long     Confirmed         Deaths     Recovered  \
    count  49068.000000  49068.000000  4.906800e+04   49068.000000  4.906800e+04   
    mean      21.433730     23.528236  1.688490e+04     884.179160  7.915713e+03   
    std       24.950320     70.442740  1.273002e+05    6313.584411  5.480092e+04   
    min      -51.796300   -135.000000  0.000000e+00       0.000000  0.000000e+00   
    25%        7.873054    -15.310100  4.000000e+00       0.000000  0.000000e+00   
    50%       23.634500     21.745300  1.680000e+02       2.000000  2.900000e+01   
    75%       41.204380     80.771797  1.518250e+03      30.000000  6.660000e+02   
    max       71.706900    178.065000  4.290259e+06  148011.000000  1.846641e+06   
    
                 Active  
    count  4.906800e+04  
    mean   8.085012e+03  
    std    7.625890e+04  
    min   -1.400000e+01  
    25%    0.000000e+00  
    50%    2.600000e+01  
    75%    6.060000e+02  
    max    2.816444e+06  
    Location: /Users/johnbahloul/Downloads/covid_data_kaggle/country_wise_latest.csv
    File Name: country_wise_latest
    Content:
    187



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
      <th>Confirmed</th>
      <th>Deaths</th>
      <th>Recovered</th>
      <th>Active</th>
      <th>New cases</th>
      <th>New deaths</th>
      <th>New recovered</th>
      <th>Deaths / 100 Cases</th>
      <th>Recovered / 100 Cases</th>
      <th>Deaths / 100 Recovered</th>
      <th>Confirmed last week</th>
      <th>1 week change</th>
      <th>1 week % increase</th>
      <th>WHO Region</th>
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
  </tbody>
</table>
</div>


    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 187 entries, 0 to 186
    Data columns (total 15 columns):
     #   Column                  Non-Null Count  Dtype  
    ---  ------                  --------------  -----  
     0   Country/Region          187 non-null    object 
     1   Confirmed               187 non-null    int64  
     2   Deaths                  187 non-null    int64  
     3   Recovered               187 non-null    int64  
     4   Active                  187 non-null    int64  
     5   New cases               187 non-null    int64  
     6   New deaths              187 non-null    int64  
     7   New recovered           187 non-null    int64  
     8   Deaths / 100 Cases      187 non-null    float64
     9   Recovered / 100 Cases   187 non-null    float64
     10  Deaths / 100 Recovered  182 non-null    float64
     11  Confirmed last week     187 non-null    int64  
     12  1 week change           187 non-null    int64  
     13  1 week % increase       187 non-null    float64
     14  WHO Region              187 non-null    object 
    dtypes: float64(4), int64(9), object(2)
    memory usage: 22.0+ KB
    None
              Confirmed         Deaths     Recovered        Active     New cases  \
    count  1.870000e+02     187.000000  1.870000e+02  1.870000e+02    187.000000   
    mean   8.813094e+04    3497.518717  5.063148e+04  3.400194e+04   1222.957219   
    std    3.833187e+05   14100.002482  1.901882e+05  2.133262e+05   5710.374790   
    min    1.000000e+01       0.000000  0.000000e+00  0.000000e+00      0.000000   
    25%    1.114000e+03      18.500000  6.265000e+02  1.415000e+02      4.000000   
    50%    5.059000e+03     108.000000  2.815000e+03  1.600000e+03     49.000000   
    75%    4.046050e+04     734.000000  2.260600e+04  9.149000e+03    419.500000   
    max    4.290259e+06  148011.000000  1.846641e+06  2.816444e+06  56336.000000   
    
            New deaths  New recovered  Deaths / 100 Cases  Recovered / 100 Cases  \
    count   187.000000     187.000000          187.000000             187.000000   
    mean     28.957219     933.812834            3.019519              64.820535   
    std     120.037173    4197.719635            3.454302              26.287694   
    min       0.000000       0.000000            0.000000               0.000000   
    25%       0.000000       0.000000            0.945000              48.770000   
    50%       1.000000      22.000000            2.150000              71.320000   
    75%       6.000000     221.000000            3.875000              86.885000   
    max    1076.000000   33728.000000           28.560000             100.000000   
    
           Deaths / 100 Recovered  Confirmed last week  1 week change  \
    count              182.000000         1.870000e+02     187.000000   
    mean                40.558297         7.868248e+04    9448.459893   
    std                336.669357         3.382737e+05   47491.127684   
    min                  0.000000         1.000000e+01     -47.000000   
    25%                  1.442500         1.051500e+03      49.000000   
    50%                  3.580000         5.020000e+03     432.000000   
    75%                  6.232500         3.708050e+04    3172.000000   
    max               3259.260000         3.834677e+06  455582.000000   
    
           1 week % increase  
    count         187.000000  
    mean           13.606203  
    std            24.509838  
    min            -3.840000  
    25%             2.775000  
    50%             6.890000  
    75%            16.855000  
    max           226.320000  
    Location: /Users/johnbahloul/Downloads/covid_data_kaggle/usa_county_wise.csv
    File Name: usa_county_wise
    Content:
    627920



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
      <th>UID</th>
      <th>iso2</th>
      <th>iso3</th>
      <th>code3</th>
      <th>FIPS</th>
      <th>Admin2</th>
      <th>Province_State</th>
      <th>Country_Region</th>
      <th>Lat</th>
      <th>Long_</th>
      <th>Combined_Key</th>
      <th>Date</th>
      <th>Confirmed</th>
      <th>Deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>16</td>
      <td>AS</td>
      <td>ASM</td>
      <td>16</td>
      <td>60.0</td>
      <td>NaN</td>
      <td>American Samoa</td>
      <td>US</td>
      <td>-14.271000</td>
      <td>-170.132000</td>
      <td>American Samoa, US</td>
      <td>1/22/20</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>316</td>
      <td>GU</td>
      <td>GUM</td>
      <td>316</td>
      <td>66.0</td>
      <td>NaN</td>
      <td>Guam</td>
      <td>US</td>
      <td>13.444300</td>
      <td>144.793700</td>
      <td>Guam, US</td>
      <td>1/22/20</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>580</td>
      <td>MP</td>
      <td>MNP</td>
      <td>580</td>
      <td>69.0</td>
      <td>NaN</td>
      <td>Northern Mariana Islands</td>
      <td>US</td>
      <td>15.097900</td>
      <td>145.673900</td>
      <td>Northern Mariana Islands, US</td>
      <td>1/22/20</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>63072001</td>
      <td>PR</td>
      <td>PRI</td>
      <td>630</td>
      <td>72001.0</td>
      <td>Adjuntas</td>
      <td>Puerto Rico</td>
      <td>US</td>
      <td>18.180117</td>
      <td>-66.754367</td>
      <td>Adjuntas, Puerto Rico, US</td>
      <td>1/22/20</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>63072003</td>
      <td>PR</td>
      <td>PRI</td>
      <td>630</td>
      <td>72003.0</td>
      <td>Aguada</td>
      <td>Puerto Rico</td>
      <td>US</td>
      <td>18.360255</td>
      <td>-67.175131</td>
      <td>Aguada, Puerto Rico, US</td>
      <td>1/22/20</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>


    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 627920 entries, 0 to 627919
    Data columns (total 14 columns):
     #   Column          Non-Null Count   Dtype  
    ---  ------          --------------   -----  
     0   UID             627920 non-null  int64  
     1   iso2            627920 non-null  object 
     2   iso3            627920 non-null  object 
     3   code3           627920 non-null  int64  
     4   FIPS            626040 non-null  float64
     5   Admin2          626792 non-null  object 
     6   Province_State  627920 non-null  object 
     7   Country_Region  627920 non-null  object 
     8   Lat             627920 non-null  float64
     9   Long_           627920 non-null  float64
     10  Combined_Key    627920 non-null  object 
     11  Date            627920 non-null  object 
     12  Confirmed       627920 non-null  int64  
     13  Deaths          627920 non-null  int64  
    dtypes: float64(3), int64(4), object(7)
    memory usage: 67.1+ MB
    None
                    UID          code3           FIPS            Lat  \
    count  6.279200e+05  627920.000000  626040.000000  627920.000000   
    mean   8.342958e+07     834.491617   33061.684685      36.707212   
    std    4.314702e+06      36.492620   18636.156825       9.061572   
    min    1.600000e+01      16.000000      60.000000     -14.271000   
    25%    8.401811e+07     840.000000   19079.000000      33.895587   
    50%    8.402921e+07     840.000000   31014.000000      38.002344   
    75%    8.404612e+07     840.000000   47131.000000      41.573069   
    max    8.410000e+07     850.000000   99999.000000      69.314792   
    
                   Long_      Confirmed         Deaths  
    count  627920.000000  627920.000000  627920.000000  
    mean      -88.601474     357.284285      17.536328  
    std        21.715747    3487.282694     300.991466  
    min      -174.159600       0.000000       0.000000  
    25%       -97.790204       0.000000       0.000000  
    50%       -89.486710       4.000000       0.000000  
    75%       -82.311265      63.000000       1.000000  
    max       145.673900  224051.000000   23500.000000  


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


