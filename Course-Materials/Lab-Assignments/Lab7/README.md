# Assignment 8: Wrangling data from APIs

## Exercises

To get full credit for this assignment, your results should include responses to the following questions:  

1. How did crime incidents for your chosen offense in your chosen month vary by city council district?  
2. Draw a chart that shows these variations.  
3. How did crime rates per 1000 residents in your chosen month vary by city council district for your chosen offense?  
4. Draw a chart that shows variations in rates by council district.  
5. Draw a line chart that shows how incidents of your chosen offense varied by day in the month that you chose.  


```python
endpoint = "https://data.fortworthtexas.gov/resource/k6ic-7kp7.json"

type_query = "?$where=offense_desc = 'Drug/Narcotic Offenses'"


date_query = " AND from_date > '2005-11-01 00:00:00' AND from_date < '2005-12-01 00:00:00' "


theft_call = endpoint + type_query + date_query

IFrame(theft_call, width = 700, height = 450)
```





        <iframe
            width="700"
            height="450"
            src="https://data.fortworthtexas.gov/resource/k6ic-7kp7.json?$where=offense_desc = 'Drug/Narcotic Offenses' AND from_date > '2005-11-01 00:00:00' AND from_date < '2005-12-01 00:00:00' "
            frameborder="0"
            allowfullscreen
        ></iframe>
        




```python
theft_call
```




    "https://data.fortworthtexas.gov/resource/k6ic-7kp7.json?$where=offense_desc = 'Drug/Narcotic Offenses' AND from_date > '2005-11-01 00:00:00' AND from_date < '2005-12-01 00:00:00' "




```python
from urllib.parse import quote

quote(theft_call, safe = "/:?$=<->")
```




    'https://data.fortworthtexas.gov/resource/k6ic-7kp7.json?$where=offense_desc%20=%20%27Drug/Narcotic%20Offenses%27%20AND%20from_date%20>%20%272005-11-01%2000:00:00%27%20AND%20from_date%20<%20%272005-12-01%2000:00:00%27%20'




```python
import pandas as pd

formatted_call = quote(theft_call, safe = "/:?$=<->")

typeOfOffense = pd.read_json(formatted_call)

typeOfOffense.shape


# import pandas as pd

# api_call = 'https://data.fortworthtexas.gov/resource/k6ic-7kp7.json?offense=23F'

# typeOfOffense = pd.read_json(api_call)

# typeOfOffense.head()
```




    (293, 17)




```python
typeOfOffense.head()
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
      <th>attempt_complete</th>
      <th>beat</th>
      <th>block_address</th>
      <th>case_no</th>
      <th>case_no_offense</th>
      <th>city</th>
      <th>councildistrict</th>
      <th>division</th>
      <th>from_date</th>
      <th>location_1</th>
      <th>location_type</th>
      <th>locationtypedescription</th>
      <th>nature_of_call</th>
      <th>offense</th>
      <th>offense_desc</th>
      <th>reported_date</th>
      <th>state</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>C</td>
      <td>C21</td>
      <td>300 BLOCK W 3RD ST</td>
      <td>50135763</td>
      <td>050135763-35A</td>
      <td>Fort Worth</td>
      <td>9.0</td>
      <td>C</td>
      <td>2005-11-01T00:00:00</td>
      <td>{'latitude': '32.754417968519874', 'human_addr...</td>
      <td>13</td>
      <td>Highway, street, roadway, alley</td>
      <td>NARC VIOL</td>
      <td>35A</td>
      <td>Drug/Narcotic Offenses</td>
      <td>2005-11-01T00:00:00</td>
      <td>TX</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C</td>
      <td>C33</td>
      <td>2000 BLOCK  YUMA ST</td>
      <td>50135857</td>
      <td>050135857-35A</td>
      <td>Fort Worth</td>
      <td>8.0</td>
      <td>C</td>
      <td>2005-11-01T00:00:00</td>
      <td>{'latitude': '32.723572451479484', 'human_addr...</td>
      <td>13</td>
      <td>Highway, street, roadway, alley</td>
      <td>NARC VIOL</td>
      <td>35A</td>
      <td>Drug/Narcotic Offenses</td>
      <td>2005-11-01T00:00:00</td>
      <td>TX</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>C31</td>
      <td>2200 BLOCK  HEMPHILL ST</td>
      <td>50136073</td>
      <td>050136073-35A</td>
      <td>Fort Worth</td>
      <td>9.0</td>
      <td>C</td>
      <td>2005-11-01T00:00:00</td>
      <td>{'latitude': '32.72047744561741', 'human_addre...</td>
      <td>3</td>
      <td>Bar, nightclub</td>
      <td>NARC VIOL</td>
      <td>35A</td>
      <td>Drug/Narcotic Offenses</td>
      <td>2005-11-01T00:00:00</td>
      <td>TX</td>
    </tr>
    <tr>
      <th>3</th>
      <td>C</td>
      <td>E42</td>
      <td>3800 BLOCK  STALCUP RD</td>
      <td>50136103</td>
      <td>050136103-35A</td>
      <td>Fort Worth</td>
      <td>5.0</td>
      <td>E</td>
      <td>2005-11-01T00:00:00</td>
      <td>{'latitude': '32.70854269712778', 'human_addre...</td>
      <td>13</td>
      <td>Highway, street, roadway, alley</td>
      <td>NARC VIOL</td>
      <td>35A</td>
      <td>Drug/Narcotic Offenses</td>
      <td>2005-11-01T00:00:00</td>
      <td>TX</td>
    </tr>
    <tr>
      <th>4</th>
      <td>C</td>
      <td>W34</td>
      <td>2700 BLOCK  RIVERPARK DR</td>
      <td>50136142</td>
      <td>050136142-35A</td>
      <td>Fort Worth</td>
      <td>3.0</td>
      <td>W</td>
      <td>2005-11-01T00:00:00</td>
      <td>{'latitude': '32.70676481163233', 'human_addre...</td>
      <td>18</td>
      <td>Parking lot, garage</td>
      <td>NARC VIOL</td>
      <td>35A</td>
      <td>Drug/Narcotic Offenses</td>
      <td>2005-11-01T00:00:00</td>
      <td>TX</td>
    </tr>
  </tbody>
</table>
</div>



### 1. 


```python
offenseByDistrict = typeOfOffense.groupby('councildistrict')

offenseByDistrict.size()
```




    councildistrict
    2.0    30
    3.0    23
    4.0    28
    5.0    50
    6.0    12
    7.0    22
    8.0    83
    9.0    43
    dtype: int64



Several of the council districts have incidents that range between 12 to 83. The highest incident of Drug/Narcotic Offenses is district 8. The lowest incident of Drug/Narcotic Offenses is district 6. 

### 2.


```python
import seaborn as sns
sns.set(style = "darkgrid", rc = {"figure.figsize": (8, 6)})

sns.countplot(data = typeOfOffense, y = 'councildistrict', order = range(2, 10))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f648f0721d0>






<img width="496" alt="a2" src="https://user-images.githubusercontent.com/11635523/50256475-0ee2f280-03bc-11e9-981f-b98a5e41b4ff.png">



### 3. 


```python
councilDistrict = pd.read_csv('http://personal.tcu.edu/kylewalker/data/cd_population.csv')

councilDistrict.columns = councilDistrict.columns.str.lower()

councilDistrict
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
      <th>name</th>
      <th>district</th>
      <th>total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2 - Salvador Espino</td>
      <td>2</td>
      <td>93845</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3 - Zim Zimmerman</td>
      <td>3</td>
      <td>93122</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4 - Cary Moon</td>
      <td>4</td>
      <td>96603</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9 - Ann Zadeh</td>
      <td>9</td>
      <td>89777</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7 - Dennis Shingleton</td>
      <td>7</td>
      <td>96199</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5 - Gyna Bivens</td>
      <td>5</td>
      <td>91467</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6 - Jungus Jordan</td>
      <td>6</td>
      <td>90365</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8 - Kelly Allen Gray</td>
      <td>8</td>
      <td>91990</td>
    </tr>
  </tbody>
</table>
</div>




```python
offenseByDistrict = pd.DataFrame(offenseByDistrict.size().reset_index())

offenseByDistrict.columns = ['district', 'count']

offenseByDistrict
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
      <th>district</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2.0</td>
      <td>30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3.0</td>
      <td>23</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.0</td>
      <td>28</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5.0</td>
      <td>50</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6.0</td>
      <td>12</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7.0</td>
      <td>22</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8.0</td>
      <td>83</td>
    </tr>
    <tr>
      <th>7</th>
      <td>9.0</td>
      <td>43</td>
    </tr>
  </tbody>
</table>
</div>




```python

councilMerged = councilDistrict.merge(offenseByDistrict, on = 'district', how = "left")

councilMerged
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
      <th>name</th>
      <th>district</th>
      <th>total</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2 - Salvador Espino</td>
      <td>2</td>
      <td>93845</td>
      <td>30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3 - Zim Zimmerman</td>
      <td>3</td>
      <td>93122</td>
      <td>23</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4 - Cary Moon</td>
      <td>4</td>
      <td>96603</td>
      <td>28</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9 - Ann Zadeh</td>
      <td>9</td>
      <td>89777</td>
      <td>43</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7 - Dennis Shingleton</td>
      <td>7</td>
      <td>96199</td>
      <td>22</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5 - Gyna Bivens</td>
      <td>5</td>
      <td>91467</td>
      <td>50</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6 - Jungus Jordan</td>
      <td>6</td>
      <td>90365</td>
      <td>12</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8 - Kelly Allen Gray</td>
      <td>8</td>
      <td>91990</td>
      <td>83</td>
    </tr>
  </tbody>
</table>
</div>




```python
councilMerged['rate'] = (councilMerged['count'] / councilMerged['total']) * 1000

councilMerged
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
      <th>name</th>
      <th>district</th>
      <th>total</th>
      <th>count</th>
      <th>rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2 - Salvador Espino</td>
      <td>2</td>
      <td>93845</td>
      <td>30</td>
      <td>0.319676</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3 - Zim Zimmerman</td>
      <td>3</td>
      <td>93122</td>
      <td>23</td>
      <td>0.246988</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4 - Cary Moon</td>
      <td>4</td>
      <td>96603</td>
      <td>28</td>
      <td>0.289846</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9 - Ann Zadeh</td>
      <td>9</td>
      <td>89777</td>
      <td>43</td>
      <td>0.478965</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7 - Dennis Shingleton</td>
      <td>7</td>
      <td>96199</td>
      <td>22</td>
      <td>0.228693</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5 - Gyna Bivens</td>
      <td>5</td>
      <td>91467</td>
      <td>50</td>
      <td>0.546645</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6 - Jungus Jordan</td>
      <td>6</td>
      <td>90365</td>
      <td>12</td>
      <td>0.132795</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8 - Kelly Allen Gray</td>
      <td>8</td>
      <td>91990</td>
      <td>83</td>
      <td>0.902272</td>
    </tr>
  </tbody>
</table>
</div>



The narcotic offense rates vary by the district. The ranges consist of 0.1 to 0.9. Previously shown in the data from questions one and two showed district 8 with the highest  incident rate. Looking at this information showing 1000 people per district/narcotic offenses continues to shows district 8 with a high rate of *0.902272.* This also includes district 6 with the lowest incident rate of *0.132795*. Districts 2, 4, 3, and 7 reside between rates 0.2 to 0.4. 

### 4


```python
council_sort = councilMerged.sort_values('rate', ascending = False)
sns.barplot(x = 'rate', y = 'name', data = council_sort)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f648d84d668>






<img width="608" alt="a4" src="https://user-images.githubusercontent.com/11635523/50256478-11454c80-03bc-11e9-9bc8-f5c2e25add4b.png">



### 5. 


```python
typeOfOffense['date1'] = typeOfOffense['from_date'].str.replace('T00:00:00', '')

typeOfOffense['date2'] = pd.to_datetime(typeOfOffense['date1'])

typeOfOffense.head()
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
      <th>attempt_complete</th>
      <th>beat</th>
      <th>block_address</th>
      <th>case_no</th>
      <th>case_no_offense</th>
      <th>city</th>
      <th>councildistrict</th>
      <th>division</th>
      <th>from_date</th>
      <th>location_1</th>
      <th>location_type</th>
      <th>locationtypedescription</th>
      <th>nature_of_call</th>
      <th>offense</th>
      <th>offense_desc</th>
      <th>reported_date</th>
      <th>state</th>
      <th>date1</th>
      <th>date2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>C</td>
      <td>C21</td>
      <td>300 BLOCK W 3RD ST</td>
      <td>50135763</td>
      <td>050135763-35A</td>
      <td>Fort Worth</td>
      <td>9.0</td>
      <td>C</td>
      <td>2005-11-01T00:00:00</td>
      <td>{'latitude': '32.754417968519874', 'human_addr...</td>
      <td>13</td>
      <td>Highway, street, roadway, alley</td>
      <td>NARC VIOL</td>
      <td>35A</td>
      <td>Drug/Narcotic Offenses</td>
      <td>2005-11-01T00:00:00</td>
      <td>TX</td>
      <td>2005-11-01</td>
      <td>2005-11-01</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C</td>
      <td>C33</td>
      <td>2000 BLOCK  YUMA ST</td>
      <td>50135857</td>
      <td>050135857-35A</td>
      <td>Fort Worth</td>
      <td>8.0</td>
      <td>C</td>
      <td>2005-11-01T00:00:00</td>
      <td>{'latitude': '32.723572451479484', 'human_addr...</td>
      <td>13</td>
      <td>Highway, street, roadway, alley</td>
      <td>NARC VIOL</td>
      <td>35A</td>
      <td>Drug/Narcotic Offenses</td>
      <td>2005-11-01T00:00:00</td>
      <td>TX</td>
      <td>2005-11-01</td>
      <td>2005-11-01</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>C31</td>
      <td>2200 BLOCK  HEMPHILL ST</td>
      <td>50136073</td>
      <td>050136073-35A</td>
      <td>Fort Worth</td>
      <td>9.0</td>
      <td>C</td>
      <td>2005-11-01T00:00:00</td>
      <td>{'latitude': '32.72047744561741', 'human_addre...</td>
      <td>3</td>
      <td>Bar, nightclub</td>
      <td>NARC VIOL</td>
      <td>35A</td>
      <td>Drug/Narcotic Offenses</td>
      <td>2005-11-01T00:00:00</td>
      <td>TX</td>
      <td>2005-11-01</td>
      <td>2005-11-01</td>
    </tr>
    <tr>
      <th>3</th>
      <td>C</td>
      <td>E42</td>
      <td>3800 BLOCK  STALCUP RD</td>
      <td>50136103</td>
      <td>050136103-35A</td>
      <td>Fort Worth</td>
      <td>5.0</td>
      <td>E</td>
      <td>2005-11-01T00:00:00</td>
      <td>{'latitude': '32.70854269712778', 'human_addre...</td>
      <td>13</td>
      <td>Highway, street, roadway, alley</td>
      <td>NARC VIOL</td>
      <td>35A</td>
      <td>Drug/Narcotic Offenses</td>
      <td>2005-11-01T00:00:00</td>
      <td>TX</td>
      <td>2005-11-01</td>
      <td>2005-11-01</td>
    </tr>
    <tr>
      <th>4</th>
      <td>C</td>
      <td>W34</td>
      <td>2700 BLOCK  RIVERPARK DR</td>
      <td>50136142</td>
      <td>050136142-35A</td>
      <td>Fort Worth</td>
      <td>3.0</td>
      <td>W</td>
      <td>2005-11-01T00:00:00</td>
      <td>{'latitude': '32.70676481163233', 'human_addre...</td>
      <td>18</td>
      <td>Parking lot, garage</td>
      <td>NARC VIOL</td>
      <td>35A</td>
      <td>Drug/Narcotic Offenses</td>
      <td>2005-11-01T00:00:00</td>
      <td>TX</td>
      <td>2005-11-01</td>
      <td>2005-11-01</td>
    </tr>
  </tbody>
</table>
</div>




```python
offense_by_date = (typeOfOffense
                .groupby('date2')
                .size()
                .reset_index()
                )

offense_by_date.columns = ["Date", "Number"]


sns.lineplot(x = "Date", y = "Number", data = offense_by_date)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f648d6f50b8>






<img width="526" alt="a5" src="https://user-images.githubusercontent.com/11635523/50256479-130f1000-03bc-11e9-9d24-1dee32405703.png">



Incidents between the 3rd and the 10th of November show the highest rate of narcotic offenses. The lowest incident is on November 24th. Offenses remained steady between the 10th - 17th.  
