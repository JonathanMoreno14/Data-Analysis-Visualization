# Assignment 6: Multivariate exploratory visualization

## Exercises

As usual, I'll ask you to do some of this on your own now in the form of a few small exercises.  Take care to answer all of the questions!  

__Exercise 1__: Explain, in your own words, the differences between a bar chart and a dot plot.  When might one of these charts be preferable to the other?  Write your response below in this Markdown cell.  



**Bar chart:** Chart/graph that has data categorized with their height and length represented by the values they represent. 

**Dot plot:** Data points that are plotted in a chart. Point's position are determined by the axis.

If the values are similar then data points are preferable. Bar charts should be used when the data has an oirgin of zero. 


---

Exercises 2 and 3 will re-use the New Mexico data that the assignment's instructions were based on.  Answer the following questions: 

__Exercise 2__: Sort your data frame by median household income in descending order.  Which county in New Mexico has the lowest median household income?  Which county has the highest median household income?  


```python
import pandas as pd
import seaborn as sns

nm = pd.read_csv("new_mexico.csv")

#nm.head()


nm_sorted = nm.sort_values(by = 'hhincome', ascending = False)
#nm_sorted.head() # Los Alamos - highest median houshold income
nm_sorted.tail() # Mora - lowest median household income

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
      <th>county</th>
      <th>hhincome</th>
      <th>pct_college</th>
      <th>median_age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20</th>
      <td>Quay</td>
      <td>28159.0</td>
      <td>15.2</td>
      <td>46.5</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Luna</td>
      <td>27326.0</td>
      <td>12.5</td>
      <td>38.4</td>
    </tr>
    <tr>
      <th>25</th>
      <td>San Miguel</td>
      <td>27000.0</td>
      <td>19.3</td>
      <td>42.2</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Guadalupe</td>
      <td>26692.0</td>
      <td>13.9</td>
      <td>41.1</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Mora</td>
      <td>21190.0</td>
      <td>13.2</td>
      <td>41.3</td>
    </tr>
  </tbody>
</table>
</div>



__Exercise 3__: Use `seaborn` to create either a dot plot or bar chart of the `"pct_college"` column for counties in New Mexico, with bars or dots sorted in descending order of educational attainment.


```python
nm_sorted = nm.sort_values('pct_college', ascending = False)
sns.barplot(x = 'pct_college', y = 'county', data = nm_sorted)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f0d67694940>






<img width="664" alt="a 4" src="https://user-images.githubusercontent.com/11635523/50254454-ac85f400-03b3-11e9-87e4-a5ab63bd2996.png">



---

In Exercises 4 and 5, you are going to examine the (potential) relationship between the percentage of the population in poverty and the percentage of households with broadband internet access for counties in Texas with populations 65,000 and up.  This information comes from the 1-year American Community Survey for 2017.  

Use the cell below to read in the dataset `texas.csv`, which is located in your assignment folder.  


```python
import pandas as pd
import seaborn as sns

tx = pd.read_csv("texas.csv")
# tx.describe()
```

__Exercise 4__: Use `seaborn` to draw a scatter plot that shows the relationship between poverty rates and broadband internet access.  


```python
sns.scatterplot(x = 'pct_poverty', y = 'pct_internet', data = tx)

```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f0d675379e8>






<img width="615" alt="a 5" src="https://user-images.githubusercontent.com/11635523/50254528-f8389d80-03b3-11e9-967b-b5c5ba269535.png">



__Exercise 5:__ Calculate the correlation coefficient for counties' poverty rates and broadband internet access.  What appears to be the relationship between the two variables?  Does this represent a _spurious_ correlation, in your opinion?


```python

tx['pct_poverty'].corr(tx['pct_internet'])
# -0.7114710892376671

sns.lmplot(x = 'pct_poverty', y = 'pct_internet', data = tx)
```

    /ext/anaconda5/lib/python3.6/site-packages/scipy/stats/stats.py:1713: FutureWarning: Using a non-tuple sequence for multidimensional indexing is deprecated; use `arr[tuple(seq)]` instead of `arr[seq]`. In the future this will be interpreted as an array index, `arr[np.array(seq)]`, which will result either in an error or a different result.
      return np.add.reduce(sorted[indexer] * weights, axis=axis) / sumval





    <seaborn.axisgrid.FacetGrid at 0x7f0d674fc2e8>






<img width="345" alt="a 6" src="https://user-images.githubusercontent.com/11635523/50254565-21f1c480-03b4-11e9-9a8a-8607e7f2e9ed.png">




```python

"""

There is a negative correlation between both poverty rates and internet access.
In regards to spurious correlation there does not seem to be a connection due to the fact the plot shows 
a negative correlation. 

"""



```




    '\n\nThere is a negative correlation between both poverty rates and internet access.\nIn regards to spurious correlation there does not seem to be a connection due to the fact the plot shows \na negative correlation. \n\n'



