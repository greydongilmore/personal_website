---
title: Operations in Python
linktitle: Operations in Python
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ml_intro:
    parent: 01. Python Basics
    weight: 1

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

The following are simple operations you can perform within python. We start with very basic operations and work up to more complex operations such as defining functions and methods

| Symbol | Task Performed |
|----|---|
| +  | Addition |
| -  | Subtraction |
| /  | division |
| %  | mod |
| *  | multiplication |
| //  | floor division |
| **  | to the power of |

## Arithmetic Operations

The following are simple math expressions that can be done in Python.

```python
# Addition
1 + 1

# Multiplication
1 * 3

# Division
1 / 2

# Square
2 ** 4

# Find remainder - called modulus
4 % 2

# Find remainder - called modulus
5 % 2

# BEDMAS
(2 + 3) * (5 + 5)
```




    2



## Variable Assignment

A name that is used to denote something or a value is called a variable. When assigning variables, the variable name should be something meaningful. This way you will remeber what it is for. Variables can not start with a number or special character. In python, variables can be declared and values can be assigned to it as follows:


```python
# I prefer sepearting words in a variable with '_', you can also use camelCase
name_of_var = 2
nameOfVar = 2

# Assign numbers to variables. These are now objects in Python.
x = 2
y = 3

# Since they are objects you can now use them to perform operations
z = x + y
z

# Multiple variables can be assigned with the same value at once
x = y = 1
print (x,y)
```

    1 1


## Strings


```python
# When using strings you can use single quotes or double quotes
'single quotes'
"double quotes"

# If you want a string to contain an apostrophe then use double quotes around the string...
" wrap lot's of other quotes"

```




    'single quotes'



## Printing variables


```python
x = 'hello'

# Use the built-in function to print variables/objects out
print(x)

# Use the format function to set the values within the string enclosed by curly braces {}
num = 12
name = 'Sam'

# Either of these methods work...
print('My number is: {one}, and my name is: {two}'.format(one=num,two=name))
print('My number is: {}, and my name is: {}'.format(num,name))
```

## Lists


```python
# With only integers
[1,2,3]

# With integers and strings
['hi',1,[1,2]]

# Adding new values to a list
my_list = ['a','b','c']
my_list.append('d')
print(my_list)

# Indexing a list by the items index
my_list[0]

# Indexing using a slice notation :
my_list[1:]

# Replace existing values in list
my_list[0] = 'NEW'
print(my_list)

# You can create nested lists as well
nest = [1,2,3,[4,5,['target']]]
nest[3]
nest[3][2]
nest[3][2][0]

```

    ['a', 'b', 'c', 'd']
    ['NEW', 'b', 'c', 'd']





    'target'



## Dictionaries


```python
d = {'key1':'item1','key2':'item2'}
d

d['key1']
```

## Booleans


```python
True
```




    True




```python
False
```




    False



## Tuples 


```python
t = (1,2,3)
t[0]

# You can not assign items to a tuple like you can with a list
t[0] = 'NEW'
```

## Sets


```python
{1,2,3}

{1,2,3,1,2,1,2,3,3,3,3,2,2,2,1,1,2}
```




    {1, 2, 3}



## Relational Operators

| Symbol | Task Performed |
|----|---|
| == | True, if it is equal |
| !=  | True, if not equal to |
| < | less than |
| > | greater than |
| <=  | less than or equal to |
| >=  | greater than or equal to |



```python
# False statements
1 > 2
'hi' == 'bye'

# True statements
1 < 2
1 >= 1
1 <= 4
1 == 1
```




    False



## Logic Operators


```python
# Using 'and' to indicate both conditions need to be True
(1 > 2) and (2 < 3)

# Using 'or' to indicate only one conditions needs to be True
(1 > 2) or (2 < 3)

# You can have as many conditional statements as you want
(1 == 2) or (2 == 3) or (4 == 4)
```




    False



## if,elif, else Statements


```python
# IF statement
if 1 < 2:
    print('Yep!')
    
# IF ELSE statement
if 1 < 2:
    print('first')
else:
    print('last')

if 1 > 2:
    print('first')
else:
    print('last')

# IF, ELIF, ELSE statement
if 1 == 2:
    print('first')
elif 3 == 3:
    print('middle')
else:
    print('Last')
```

    Yep!


## For Loops


```python
seq = [1,2,3,4,5]
for item in seq:
    print(item)
    
for item in seq:
    print('Yep')

# You can name the iterator whatever you like
for jelly in seq:
    print(jelly+jelly)
    
```

## While Loops


```python
i = 1
while i < 5:
    print('i is: {}'.format(i))
    i = i+1
```

    i is: 1
    i is: 2
    i is: 3
    i is: 4


## range() function


```python
range(5)

# Great for using in For loops
for i in range(5):
    print(i)

# You can use it to create lists
list(range(5))
```




    range(0, 5)



## List comprehension


```python
x = [1,2,3,4]

# Perform operations within a For loop and append the outputs to a list object
out = []
for item in x:
    out.append(item**2)
print(out)
```

A very useful technique in Python is the one line for loop:


```python
[item**2 for item in x]
```

## Defining functions


```python
def my_func(param1='default'):
    """
    Docstring goes here.
    """
    print(param1)

# To call your function you need to include brackets at the end
my_func

my_func()
```

Now that you have defined your function with an input you can provide new inputs to the function to perform an operation


```python
# You can either call the defined input varible for your function
my_func(param1='new param')

# Or you can just provide the input, remember if you have multiple function inputs the position of these inputs matter!
my_func('new param')
```

    new param



```python
# Use the 'Return' function to return a value from within your function and assign it to a variable
def square(x):
    return x**2

out = square(2)
print(out)
```

## Lambda, map and filter

Instead of writing a function you can use the lambda function instead:


```python
def times2(var):
    return var*2

times2(2)

# lambda
lambda var: var*2

# map
seq = [1,2,3,4,5]
map(times2,seq)

# Combining lambda and map together you get
list(map(times2,seq))

# Here is more detail
list(map(lambda var: var*2,seq))

# Using the filter function to return values that meet a condition
filter(lambda item: item%2 == 0,seq)
list(filter(lambda item: item%2 == 0,seq))
```




    [2, 4]



## Methods

One of the most useful aspects of the Python language is that everything is an object and has inherent methods.

### string methods


```python
# Assign 'st' to be a string
st = 'hello my name is Sam'

# A string type in Python has several methods
# To return all lowercase
st.lower()

# All uppercase
st.upper()

# Split the string at white spaces
st.split()

# You can use the split method to split at a character you want
tweet = 'Go Sports! #Sports'
tweet.split('#')

# You can return only the part of the string you want after the split method
tweet.split('#')[1]
```

### dictionary methods


```python
d = {'key1': 'item1', 'key2': 'item2'}

# Print the keys in a dictionary
d.keys()

# Print the items in a dictionary
d.items()
```




    dict_keys(['key1', 'key2'])



### list methods


```python
lst = [1,2,3]

lst.pop()
lst

# Find a value within a list
'x' in [1,2,3]

'x' in ['x','y','z']
```
