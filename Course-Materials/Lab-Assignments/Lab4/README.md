# Assignment 5: Univariate data analysis

## Exercises

Now it's time to test what you've learned!  In the following exercises, you'll apply the techniques you've learned in this notebook to a new dataset from the Kaiser Family Foundation, which measures childhood overweight & obesity rates by state.  The data file is named `child_data.csv` and is found in your Assignment 5 directory.  Follow the same steps to read it in - fortunately it is formatted the same way as the previous dataset.  Load in the new dataset as a `pandas` DataFrame, and respond to the following questions: 

__Exercise 1:__ What are the mean and median values for childhood overweight/obesity rates for states in the US?  


```python
import  pandas as pd

# df = pd.DataFrame()
# print(df)
obesityData = pd.read_csv("child_data.csv")

print(obesityData.rate.mean())
print(obesityData.rate.median())
```

    0.30788235294117644
    0.304


__Exercise 2__: What are the minimum and maximum values for childhood overweight/obesity rates?  What is the range?  


```python
# obesityData.rate.min()
# obesityData.rate.max()
# obesityData.range()

print(obesityData.rate.min())
print(obesityData.rate.max())

range = obesityData.rate.max() - obesityData.rate.min()
print(range)
```

    0.221
    0.39799999999999996
    0.17699999999999996


__Exercise 3__: Draw a histogram of childhood overweight/obesity rates.  Do your data appear to be skewed in one direction or another?  


```python
import seaborn as sns
sns.set_style("darkgrid")

obesityData.rate.hist()

'''
The Data appears to be a normal curve, it does not appear to be skewed. 
'''
sns.distplot(obesityData.rate)
```

    /ext/anaconda5/lib/python3.6/site-packages/scipy/stats/stats.py:1713: FutureWarning: Using a non-tuple sequence for multidimensional indexing is deprecated; use `arr[tuple(seq)]` instead of `arr[seq]`. In the future this will be interpreted as an array index, `arr[np.array(seq)]`, which will result either in an error or a different result.
      return np.add.reduce(sorted[indexer] * weights, axis=axis) / sumval





    <matplotlib.axes._subplots.AxesSubplot at 0x7fba1da438d0>






<img width="364" alt="a 3" src="https://user-images.githubusercontent.com/11635523/50253996-fa016180-03b1-11e9-9242-4ce6b18e7b3c.png">



__Exercise 4__: Draw a box plot of childhood overweight/obesity rates.  


```python
sns.boxplot(obesityData.rate, color = "blue", orient = "v")
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7fba1d9bf358>






<img width="400" alt="a 1" src="https://user-images.githubusercontent.com/11635523/50253893-9a0abb00-03b1-11e9-817f-05f52538be66.png">



__Exercise 5:__: You pick: draw either a kernel density plot or a violin plot with your data.  Change the color of the plot to orange, and shade the area beneath the density curve if you select a density plot.  


```python
sns.kdeplot(obesityData.rate, shade = True, color = "orange")
```

    /ext/anaconda5/lib/python3.6/site-packages/scipy/stats/stats.py:1713: FutureWarning: Using a non-tuple sequence for multidimensional indexing is deprecated; use `arr[tuple(seq)]` instead of `arr[seq]`. In the future this will be interpreted as an array index, `arr[np.array(seq)]`, which will result either in an error or a different result.
      return np.add.reduce(sorted[indexer] * weights, axis=axis) / sumval





    <matplotlib.axes._subplots.AxesSubplot at 0x7fba1d980630>







<img width="364" alt="a 2" src="https://user-images.githubusercontent.com/11635523/50253972-e2c27400-03b1-11e9-8eca-4239536c41c2.png">




```python

```
