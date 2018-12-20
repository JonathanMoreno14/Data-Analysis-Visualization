# Assignment 9: Data visualization

## Exercises

To get credit for this assignment, you are going to apply what you've learned to some additional tasks using the baby names dataset.  Some of this will involve re-producing some of the analyses in the notebook, but for different prompts.  

__Exercise 1:__ Re-create the heatmap from Question 1, but this time for females.  What trends do you observe?  


```python
female15 = df[(df.year == 2015) & (df.sex == 'F')]
female15sorted = female15.sort_values('n', ascending = False)
top_female = female15sorted[0:15]
name_list = top_female.name.tolist()

name_list
```




    ['Emma',
     'Olivia',
     'Sophia',
     'Ava',
     'Isabella',
     'Mia',
     'Abigail',
     'Emily',
     'Charlotte',
     'Harper',
     'Madison',
     'Amelia',
     'Elizabeth',
     'Sofia',
     'Evelyn']




```python
sub1 = df[(df.name.isin(name_list)) & (df.year > 1999) & (df.sex == 'F')]

sub1['per1000'] = sub1.prop * 1000

sub1.head()
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
      <th>year</th>
      <th>sex</th>
      <th>name</th>
      <th>n</th>
      <th>prop</th>
      <th>per1000</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1332606</th>
      <td>2000</td>
      <td>F</td>
      <td>Emily</td>
      <td>25953</td>
      <td>0.013013</td>
      <td>13.012538</td>
    </tr>
    <tr>
      <th>1332608</th>
      <td>2000</td>
      <td>F</td>
      <td>Madison</td>
      <td>19967</td>
      <td>0.010011</td>
      <td>10.011226</td>
    </tr>
    <tr>
      <th>1332614</th>
      <td>2000</td>
      <td>F</td>
      <td>Elizabeth</td>
      <td>15089</td>
      <td>0.007565</td>
      <td>7.565453</td>
    </tr>
    <tr>
      <th>1332619</th>
      <td>2000</td>
      <td>F</td>
      <td>Abigail</td>
      <td>13087</td>
      <td>0.006562</td>
      <td>6.561673</td>
    </tr>
    <tr>
      <th>1332621</th>
      <td>2000</td>
      <td>F</td>
      <td>Olivia</td>
      <td>12852</td>
      <td>0.006444</td>
      <td>6.443846</td>
    </tr>
  </tbody>
</table>
</div>




```python
wide1 = sub1.pivot(index = 'name', columns = 'year', values = 'per1000')

sns.heatmap(wide1)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f974cd47208>






<img width="711" alt="e1" src="https://user-images.githubusercontent.com/11635523/50259847-6f2d6080-03cb-11e9-85f3-5d4073314895.png">




```python
import matplotlib.pyplot as plt

sns.heatmap(wide1, annot = True, cmap = 'Blues')

plt.xticks(rotation = 45)
plt.ylabel("")
plt.xlabel("")
plt.title("Most popular baby names - Female (rate per 1000)")
```




    Text(0.5,1,'Most popular baby names - Female (rate per 1000)')






<img width="695" alt="e1 part 2" src="https://user-images.githubusercontent.com/11635523/50259849-72c0e780-03cb-11e9-99d6-a9907da86d89.png">



The trends in the heatmap show Emily and Madison have been popular names. Names like Emma and Olivia have been popular in 2014 and 2015. Another trend that is shown is with the name Emma. The popularity of the name ranged from 2012 through 2015. 

__Exercise 2:__ Create a line chart that shows how a name of your choice has varied in popularity over time.  Find out the year when your chosen name peaked in popularity, and annotate your chart to show where this peak is located on the line.  


```python
sns.set_style("darkgrid")
chosenName = ['Jonathan']

chosenName_df = df[(df.name.isin(chosenName)) & (df.sex == 'M') & (df.year > 1979)]

chosenName_df['per1000'] = chosenName_df.prop * 1000

chosenName_df.head()
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
      <th>year</th>
      <th>sex</th>
      <th>name</th>
      <th>n</th>
      <th>prop</th>
      <th>per1000</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>875943</th>
      <td>1980</td>
      <td>M</td>
      <td>Jonathan</td>
      <td>18992</td>
      <td>0.010240</td>
      <td>10.239975</td>
    </tr>
    <tr>
      <th>895409</th>
      <td>1981</td>
      <td>M</td>
      <td>Jonathan</td>
      <td>22597</td>
      <td>0.012135</td>
      <td>12.135354</td>
    </tr>
    <tr>
      <th>915015</th>
      <td>1982</td>
      <td>M</td>
      <td>Jonathan</td>
      <td>23124</td>
      <td>0.012256</td>
      <td>12.256295</td>
    </tr>
    <tr>
      <th>934439</th>
      <td>1983</td>
      <td>M</td>
      <td>Jonathan</td>
      <td>22744</td>
      <td>0.012210</td>
      <td>12.209505</td>
    </tr>
    <tr>
      <th>953942</th>
      <td>1984</td>
      <td>M</td>
      <td>Jonathan</td>
      <td>23327</td>
      <td>0.012436</td>
      <td>12.436185</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.lineplot(data = chosenName_df, x = "year", y = "per1000", hue = "name")
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f974cc004a8>






<img width="727" alt="exercise 2 part 1" src="https://user-images.githubusercontent.com/11635523/50259990-0f838500-03cc-11e9-9bde-020b8867ff0c.png">




```python
name_yrs = {'Jonathan': 1985}

for chosenName, year in name_yrs.items():
    subset = chosenName_df[(chosenName_df.name == chosenName) & (chosenName_df.year == year)]
    value = subset.per1000.values[0]
    print(chosenName + ': ' + str(value))
```

    Jonathan: 12.540580111014288



```python
sns.lineplot(data = chosenName_df, x = "year", y = "per1000", hue = "name")

plt.annotate('Jonathan', xy = (1985, 12.5), xycoords = 'data', 
            xytext = (1985, 12), textcoords = 'data', arrowprops = dict(arrowstyle = 'simple'),
            fontsize = 10)

plt.ylabel("The name Jonathan per 1000", fontsize = 12)
plt.xlabel("")
plt.title("The popularity of the Name: Jonathan", fontsize = 15)
plt.legend(title = "", fontsize = 12)
```




    <matplotlib.legend.Legend at 0x7f974c933b00>






<img width="727" alt="exercise 2 part 2" src="https://user-images.githubusercontent.com/11635523/50259993-16aa9300-03cc-11e9-9d17-c86308fa81b4.png">



__Exercise 3:__ In Question 2, we looked at the possible influence of Disney princess movies on female baby names.  Pick four other names (male or female) from popular culture over the past 30 years and produce a chart that illustrates their influence (or lack thereof) on baby names.  Be strategic with your name decisions!  You can create a single line chart with four series, or a small multiples chart with facets - pick the one you think is ideal!


```python
sns.set_style("darkgrid")
chosenNames = ['Leonard', 'Sheldon', 'Howard', 'Stuart']

chosenNames_df = df[(df.name.isin(chosenNames)) & (df.sex == 'M') & (df.year > 1979)]

chosenNames_df['per1000'] = chosenNames_df.prop * 1000

chosenNames_df.head()
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
      <th>year</th>
      <th>sex</th>
      <th>name</th>
      <th>n</th>
      <th>prop</th>
      <th>per1000</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>876115</th>
      <td>1980</td>
      <td>M</td>
      <td>Leonard</td>
      <td>1277</td>
      <td>0.000689</td>
      <td>0.688524</td>
    </tr>
    <tr>
      <th>876164</th>
      <td>1980</td>
      <td>M</td>
      <td>Howard</td>
      <td>923</td>
      <td>0.000498</td>
      <td>0.497657</td>
    </tr>
    <tr>
      <th>876257</th>
      <td>1980</td>
      <td>M</td>
      <td>Stuart</td>
      <td>561</td>
      <td>0.000302</td>
      <td>0.302476</td>
    </tr>
    <tr>
      <th>876391</th>
      <td>1980</td>
      <td>M</td>
      <td>Sheldon</td>
      <td>321</td>
      <td>0.000173</td>
      <td>0.173075</td>
    </tr>
    <tr>
      <th>895601</th>
      <td>1981</td>
      <td>M</td>
      <td>Leonard</td>
      <td>1191</td>
      <td>0.000640</td>
      <td>0.639607</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.lineplot(data = chosenNames_df, x = "year", y = "per1000", hue = "name")
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f974c97d550>






![png](data-visualization_files/data-visualization_40_1.png)


