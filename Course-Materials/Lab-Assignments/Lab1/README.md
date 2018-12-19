## Programming I - Intro to Python



__Exercise 2__: Assign the number 31 to a new variable, `q`.  Write an expression that raises q to the 4th power and run the cell.  


```python
q = 31
q ** 4
```




    923521



__Exercise 3__: Create a new variable named `smu` by assigning the lowercase string 'southern methodist university' to it.  Use Python string methods to capitalize your string appropriately.  Add a comment in your code that explains what you did.  


```python
smu = "southern methodist university"
smu.title()
# Used the title() method to capitalize the first letter of each word of string 
```




    'Southern Methodist University'



__Exercise 4__: Assign the list `['a', 'b', 'c', 'd', 'e']` to a variable.  Reverse the list, then insert 'z' at index 3, and finally append 'o' to the end.


```python
list = ['a', 'b', 'c', 'd', 'e']
list.reverse()
list
list.insert(3, 'z')
list.append('o')
list
```




    ['e', 'd', 'c', 'z', 'b', 'a', 'o']



__Exercise 5__: (Modified from your textbook): A string slice can use an optional third index to specify the 'step size', which refers to the number of spaces between characters.  Your textbook gives the following example: 


```python
fruit = 'banana'

fruit[0:5:2]
```




    'bnn'



The same result could be achieved, however, by omitting the 5, as the above example uses the whole string: 


```python
fruit[0::2]
```




    'bnn'



In the cell below, I will provide you with a string of characters that may appear quite random at first.  Run the cell to assign the string to the variable `code`.  However, the string is in reality an encoded message, in which the character to keep is at __every fourth character__.

Use Python string slicing to decode the message, and print the result to your notebook.  The result is a familar expression, so if you are not getting a result that makes sense, try again! 

__Hint__: remember rules about Python indexing, which starts at 0, not 1!


```python
code = 'varCjjlopaxntrrgnbXrOPraiiItUuUuzaQlliyaxx*t#rgiffFoce&ntPls87C!'
```


```python

```


```python
# Your answer goes here!
# print(code[4::5])
# jarriuQa#f&s

print(code[3::4])
# Congratulations!
```

    Congratulations!



```python

```
