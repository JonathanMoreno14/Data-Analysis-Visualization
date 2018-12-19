# Programming II: Functions and modules in Python

## Exercises

As with the previous Jupyter Notebook you worked with, I'll ask you to complete a series of small exercises below to get full credit for this week's assignment.  Some of these exercises will build upon the skills you learned last week - so be prepared!

__Exercise 1:__ Explain, in your own words, the difference between using `print` and `return` for the output of a function.  Write your response below, in this Markdown cell.  


**print** - Print produces an output from the function the difference between both is *print* does not correspond to the function. It's not part of the function. Unlike *return*, it returns a value associated with the actual workings of the function

**return** - Return, returns a value from the function


__Exercise 2:__ Write a function called `make_big` that takes a lowercase string as input and prints the string with all capital letters.  Create a new variable and assign to it a string with all lowercase letters, then call the `make_big` function with that variable as its argument.  


```python
# Your answer goes here!
string = "hello world"
def make_big(str):
    return str.upper()

make_big(string)
```




    'HELLO WORLD'



__Exercise 3:__ (Adapted from your textbook) Python provides a built-in function called `len` that returns the length of a string.  For example: 


```python
len('Texas Christian University')
```




    26



Additionally, Python includes built-in string methods called `ljust` and `rjust` that fill in a string with a specified character the left or right hand side so that the string attains a specified length.  For example: 


```python
ks = 'Kansas'

ks.rjust(15, 'I')
```




    'IIIIIIIIIKansas'



As the string `'Kansas'` has six characters, passing `(15, 'I')` to `rjust` adds nine `I`s to the left of `Kansas`.  

Your job is now to write a function named `right_justify` that takes a string named `s` as a parameter and prints the string with enough leading spaces so that the last letter of the string is in column 70 of the display.  For example: 

```python

right_justify(s = 'kyle')

                                                              kyle # the result
                                                              
```

Write the function in the cell below, then run the function to show that it works.  


```python
# Your answer goes here!
s = "s"
def right_justify(spaces):
       return spaces.rjust(70)
        
right_justify(s)
    

```




    '                                                                     s'



__Exercise 4:__  Write a function called `first_word` that takes a list of character strings as input and returns the first element of the list in alphabetical order.  For example, your function should work like this: 

```python

students = ['Mary', 'Zelda', 'Jimmy', 'Jack', 'Bartholomew', 'Gertrude']

first_word(students)

'Bartholomew' # The result

```

_Hint:_ You'll need to first sort your list in the function to accomplish this, then identify the first element.  Within a function, it is a good idea to use multiple lines of code to separate out the different steps.  Just make sure all the code that belongs to the function is indented!

After you've written the function, run it by supplying the list `teams` to your function as an argument to test it.  


```python
teams = ['Stars', 'Cowboys', 'Rangers', 'Mavericks', 'FC Dallas']

# Your code goes below!
def first_word(texasTeams):
    texasTeams.sort()
    return texasTeams[0]    

first_word(teams)
```




    'Cowboys'



__Exercise 5:__ Create a new Python script and save it in your notebook directory.  In the script, you'll write a new function called `get_word`.  This function should have two parameters.  The first should take an input list of character strings, as in Exercise 4; the second parameter should take the index of the character string you'd like to return from the list.  You don't need to worry about sorting the list this time.  

For example: 

```python

get_word(students, 3)

'Jack' # The result

```

Your code in the cell below should: 

1. Import your `get_word` function into your Python session, using one of the specified methods for importing modules that you've learned in this notebook; 
2. Call the function with `mascots` as the first argument so that it returns 'Horned Frogs', and assign the result to a new variable; 
3. Print your new variable to make sure you've done everything correctly - if you have, it should print 'Horned Frogs'.  



```python
mascots = ["Sooners", "Mountaineers", "Longhorns", "Bears", "Cowboys", "Horned Frogs", "Wildcats", "Cyclones", "Red Raiders", "Jayhawks"]

# Your code goes below!
from exercise5module import *

str = get_word(mascots, 5)

print(str)
```

    Horned Frogs


For full credit, your assignment folder must include the completed Jupyter notebook and your Python script.  
