# Assignment 7: Data wrangling I

## Exercises

You'll now complete some exercises so you can practice what you've learned.  Your job, in general, is to replicate the analysis above, but for a different column in the dataset.  You'll be analyzing the column `PCTPELL`, which denotes the percentages of students receiving Pell Grants, a federal grant program to help students pay for college.  Unlike loans, Pell Grants do not need to be repaid.  

While you'll be using a lot of the code I provided for you and modifying it slightly, make sure that you know what the code is doing at every step!  You'll want to get this practice in before the second take-home exam. 

---

__Exercise 1__:  Similar to what you did earlier in the notebook, create a data frame that is subsetted for the columns `'INSTNM', 'STABBR', 'PREDDEG', 'CONTROL', 'UGDS',` and `'PCTPELL'`, and that retains only those rows where `PREDDEG` is equal to `3`, representing primarily bachelor's-granting universities.  What is the mean, median, maximum value, and minimum value of the `PCTPELL` column?  


```python
import pandas as pd

full_url = 'http://personal.tcu.edu/kylewalker/data/colleges.csv'
full = pd.read_csv(full_url, encoding = 'latin_1')

arrayColumns = ['INSTNM', 'STABBR', 'PREDDEG', 'CONTROL', 'UGDS','PCTPELL']


df = full[arrayColumns]
df = df.rename(columns = {'STABBR': 'STATE'})

bGU = df[df['PREDDEG'] == 3]
bGU.head()


#df.head()
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
      <th>INSTNM</th>
      <th>STATE</th>
      <th>PREDDEG</th>
      <th>CONTROL</th>
      <th>UGDS</th>
      <th>PCTPELL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alabama A &amp; M University</td>
      <td>AL</td>
      <td>3</td>
      <td>1</td>
      <td>4051.0</td>
      <td>0.7115</td>
    </tr>
    <tr>
      <th>1</th>
      <td>University of Alabama at Birmingham</td>
      <td>AL</td>
      <td>3</td>
      <td>1</td>
      <td>11200.0</td>
      <td>0.3505</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Amridge University</td>
      <td>AL</td>
      <td>3</td>
      <td>2</td>
      <td>322.0</td>
      <td>0.6839</td>
    </tr>
    <tr>
      <th>3</th>
      <td>University of Alabama in Huntsville</td>
      <td>AL</td>
      <td>3</td>
      <td>1</td>
      <td>5525.0</td>
      <td>0.3281</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alabama State University</td>
      <td>AL</td>
      <td>3</td>
      <td>1</td>
      <td>5354.0</td>
      <td>0.8265</td>
    </tr>
  </tbody>
</table>
</div>




```python
# PCTPELL column
# mean, median, maximum value, and minimum value

# groupOne = bGU.groupby('PCTPELL')
#type(groupsOne)

#groupsOne.PCTPELL.mean()

#pellGrouped = bGU.groupby('PCTPELL')

```


```python
# Mean:
#pellGrouped['PCTPELL'].mean()
bGU.PCTPELL.mean()
```




    0.4188518779342721




```python
# Median:
#pellGrouped['PCTPELL'].median()
bGU.PCTPELL.median()
```




    0.3943




```python
# Max:
#pellGrouped['PCTPELL'].max()
bGU.PCTPELL.max()
```




    1.0




```python
# Min:
#pellGrouped['PCTPELL'].min()
bGU.PCTPELL.min()
```




    0.0



__Exercise 2:__ How many null values are contained in the `PCTPELL` column in your subsetted data frame?  Once you've found this out, drop them from your data frame.  


```python
nullValues = pd.isnull(bGU.PCTPELL)

bguNull = bGU[nullValues]

bguNull.shape
```




    (3, 6)




```python
bguNull
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
      <th>INSTNM</th>
      <th>STATE</th>
      <th>PREDDEG</th>
      <th>CONTROL</th>
      <th>UGDS</th>
      <th>PCTPELL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1171</th>
      <td>Rosalind Franklin University of Medicine and S...</td>
      <td>IL</td>
      <td>3</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1893</th>
      <td>New England College of Optometry</td>
      <td>MA</td>
      <td>3</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5856</th>
      <td>San Diego State University-Imperial Valley Campus</td>
      <td>CA</td>
      <td>3</td>
      <td>1</td>
      <td>693.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
dataFrameUpdated = bGU.dropna()

dataFrameUpdated.shape
```




    (2130, 6)



__Exercise 3:__ Compare the means of `PCTPELL` by the different groups of `CONTROL` (the college/university type).  Draw a visualization that shows how the distributions vary.  


```python
groupsOne = dataFrameUpdated.groupby('CONTROL')

type(groupsOne)
```




    pandas.core.groupby.groupby.DataFrameGroupBy




```python
groupsOne.PCTPELL.mean()
```




    CONTROL
    1    0.386187
    2    0.394408
    3    0.588575
    Name: PCTPELL, dtype: float64




```python
import seaborn as sns
sns.set(style = "darkgrid", rc = {"figure.figsize": (10, 8)})

sns.violinplot(data = dataFrameUpdated, x = 'CONTROL', y = 'PCTPELL')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f24f44a1128>






<img width="619" alt="exercise 3" src="https://user-images.githubusercontent.com/11635523/50255056-07204f80-03b6-11e9-80b3-0f8b4f010360.png">



__Exercise 4:__ Draw a visualization that breaks your visualization from Exercise 3 down by state with `catplot`, similar to what you did earlier in the notebook; in this instance, however, compare Texas with Florida and Illinois.  


```python
sub1 = dataFrameUpdated[dataFrameUpdated.STATE.isin(['TX', 'FL', 'IL'])]

sns.catplot(data = sub1, x = 'CONTROL', y = 'PCTPELL',
               col = 'STATE', kind = 'violin', order = [1, 2, 3])
```




    <seaborn.axisgrid.FacetGrid at 0x7f24f44febe0>






<img width="1065" alt="exercise 4" src="https://user-images.githubusercontent.com/11635523/50255114-4189ec80-03b6-11e9-8eb5-e2d9530e2d7e.png">



__Exercise 5__: Show how the percent of students receiving Pell Grants varies by institution size and institution type (public, private, for-profit).  Break up the `UGDS` column into five quantiles in your data frame as you did before, and then compare the means of `PCTPELL` by institution type by institution size.  Draw a visualization with `catplot` to show this graphically.  


```python
# PCTPELL, which denotes the percentages of students receiving Pell Grants, a federal grant program to help students pay for college.
# CONTROL: The ownership of the institution, coded as 1 for public non-profit, 2 for private non-profit, and 3 for private for-profit;
# UGDS: The number of undergraduates enrolled at the institution;

sns.lmplot(data = dataFrameUpdated, x = 'UGDS', y = 'PCTPELL')

```




    <seaborn.axisgrid.FacetGrid at 0x7f25043cc320>






<img width="333" alt="exercise 5 part 1" src="https://user-images.githubusercontent.com/11635523/50255171-6d0cd700-03b6-11e9-88c6-b8bd014a940e.png">





```python
sns.lmplot(data = dataFrameUpdated, x = 'CONTROL', y = 'PCTPELL')
```




    <seaborn.axisgrid.FacetGrid at 0x7f24f450c1d0>






<img width="345" alt="exercise 5 part 2" src="https://user-images.githubusercontent.com/11635523/50255239-bc530780-03b6-11e9-82b5-16bf8451920c.png">




```python
# UGDS: The number of undergraduates enrolled at the institution;

dataFrameUpdated['quant5'] = pd.qcut(dataFrameUpdated.UGDS, 5, labels = range(1, 6))

dataFrameUpdated.head()
```

    /usr/local/lib/python3.6/dist-packages/ipykernel/__main__.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      app.launch_new_instance()





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
      <th>INSTNM</th>
      <th>STATE</th>
      <th>PREDDEG</th>
      <th>CONTROL</th>
      <th>UGDS</th>
      <th>PCTPELL</th>
      <th>quant5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alabama A &amp; M University</td>
      <td>AL</td>
      <td>3</td>
      <td>1</td>
      <td>4051.0</td>
      <td>0.7115</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>University of Alabama at Birmingham</td>
      <td>AL</td>
      <td>3</td>
      <td>1</td>
      <td>11200.0</td>
      <td>0.3505</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Amridge University</td>
      <td>AL</td>
      <td>3</td>
      <td>2</td>
      <td>322.0</td>
      <td>0.6839</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>University of Alabama in Huntsville</td>
      <td>AL</td>
      <td>3</td>
      <td>1</td>
      <td>5525.0</td>
      <td>0.3281</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alabama State University</td>
      <td>AL</td>
      <td>3</td>
      <td>1</td>
      <td>5354.0</td>
      <td>0.8265</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
compareGroup = dataFrameUpdated.groupby(['CONTROL', 'quant5'])

compareGroup.PCTPELL.mean()
```




    CONTROL  quant5
    1        1         0.276178
             2         0.373557
             3         0.416581
             4         0.432808
             5         0.363917
    2        1         0.459126
             2         0.454957
             3         0.368640
             4         0.317116
             5         0.287045
    3        1         0.615777
             2         0.580589
             3         0.582105
             4         0.533914
             5         0.510368
    Name: PCTPELL, dtype: float64




```python
# Break up the UGDS column into five quantiles in your data frame as you did before, and then compare the means of PCTPELL by institution type by institution size. Draw a visualization with catplot to show this graphically.

sns.catplot(data = dataFrameUpdated, x = 'PCTPELL', y = 'quant5', col = 'CONTROL', kind = 'bar')
```




    <seaborn.axisgrid.FacetGrid at 0x7f25040ad630>






<img width="1064" alt="exercise 5 part 3" src="https://user-images.githubusercontent.com/11635523/50255272-dbea3000-03b6-11e9-94e8-fb2886d3083c.png">


