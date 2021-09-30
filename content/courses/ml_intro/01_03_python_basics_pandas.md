---
title: Pandas
linktitle: Pandas
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ml_intro:
    parent: 01. Python Basics
    weight: 3

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3
---

Pandas is a newer package built on top of NumPy, and provides an efficient implementation of a **DataFrame**. **DataFrames** are essentially multidimensional arrays with attached row and column labels, and often with heterogeneous types and/or missing data. As well as offering a convenient storage interface for labeled data, Pandas implements a number of powerful data operations familiar to users of both database frameworks and spreadsheet programs.

At the very basic level, Pandas objects can be thought of as enhanced versions of NumPy structured arrays in which the rows and columns are identified with labels rather than simple integer indices. As we will see during the course of this chapter, Pandas provides a host of useful tools, methods, and functionality on top of the basic data structures, but nearly everything that follows will require an understanding of what these structures are. Thus, before we go any further, let's introduce these three fundamental Pandas data structures: the Series, DataFrame, and Index.

## Series

The first main data type we will learn about for pandas is the Series data type. Let's import Pandas and explore the Series object. A Series is very similar to a NumPy array (in fact it is built on top of the NumPy array object). What differentiates the NumPy array from a Series, is that a Series can have axis labels, meaning it can be indexed by a label, instead of just a number location. It also doesn't need to hold numeric data, it can hold any arbitrary Python Object.

Let's explore this concept through some examples:

```python
import numpy as np
import pandas as pd
```

You can convert a list,numpy array, or dictionary to a Series:

```python
labels = ['a','b','c']
my_list = [10,20,30]
arr = np.array([10,20,30])
d = {'a':10,'b':20,'c':30}
```

** Using Lists**

```python
pd.Series(data=my_list)
```

    0    10
    1    20
    2    30
    dtype: int64

```python
pd.Series(data=my_list,index=labels)
```

    a    10
    b    20
    c    30
    dtype: int64

```python
pd.Series(my_list,labels)
```

    a    10
    b    20
    c    30
    dtype: int64

** NumPy Arrays **

```python
pd.Series(arr)
```

    0    10
    1    20
    2    30
    dtype: int64

```python
pd.Series(arr,labels)
```

    a    10
    b    20
    c    30
    dtype: int64

** Dictionary**

```python
pd.Series(d)
```

    a    10
    b    20
    c    30
    dtype: int64

### Data in a Series

A pandas Series can hold a variety of object types:

```python
pd.Series(data=labels)
```

    0    a
    1    b
    2    c
    dtype: object


```python
# Even functions (although unlikely that you will use this)
pd.Series([sum,print,len])
```

    0      <built-in function sum>
    1    <built-in function print>
    2      <built-in function len>
    dtype: object

### Using an Index

The key to using a Series is understanding its index. Pandas makes use of these index names or numbers by allowing for fast look ups of information (works like a hash table or dictionary).

Let's see some examples of how to grab information from a Series. Let us create two sereis, ser1 and ser2:

```python
ser1 = pd.Series([1,2,3,4],index = ['USA', 'Germany','USSR', 'Japan'])                                   
```

```python
ser1
```

    USA        1
    Germany    2
    USSR       3
    Japan      4
    dtype: int64

```python
ser2 = pd.Series([1,2,5,4],index = ['USA', 'Germany','Italy', 'Japan'])                                   
```

```python
ser2
```

    USA        1
    Germany    2
    Italy      5
    Japan      4
    dtype: int64

```python
ser1['USA']
```

    1

Operations are then also done based off of index:

```python
ser1 + ser2
```

    Germany    4.0
    Italy      NaN
    Japan      8.0
    USA        2.0
    USSR       NaN
    dtype: float64

Let's stop here for now and move on to DataFrames, which will expand on the concept of Series!

## DataFrames

DataFrames are the workhorse of pandas and are directly inspired by the R programming language. We can think of a DataFrame as a bunch of Series objects put together to share the same index. Let's use pandas to explore this topic!

```python
import pandas as pd
import numpy as np
```

```python
from numpy.random import randn
np.random.seed(101)
```

```python
df = pd.DataFrame(randn(5,4),index='A B C D E'.split(),columns='W X Y Z'.split())
```

```python
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>
</div>


### Selection and Indexing

Let's learn the various methods to grab data from a DataFrame

```python
df['W']
```

    A    2.706850
    B    0.651118
    C   -2.018168
    D    0.188695
    E    0.190794
    Name: W, dtype: float64

```python
# Pass a list of column names
df[['W','Z']]
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>-0.589001</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>
</div>

```python
# SQL Syntax (NOT RECOMMENDED!)
df.W
```

    A    2.706850
    B    0.651118
    C   -2.018168
    D    0.188695
    E    0.190794
    Name: W, dtype: float64

DataFrame Columns are just Series

```python
type(df['W'])
```

    pandas.core.series.Series

#### Creating a new column

```python
df['new'] = df['W'] + df['Y']
```

```python
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
      <th>new</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
      <td>3.614819</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
      <td>-0.196959</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
      <td>-1.489355</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
      <td>-0.744542</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
      <td>2.796762</td>
    </tr>
  </tbody>
</table>
</div>

#### Removing Columns

```python
df.drop('new',axis=1)
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>
</div>

```python
# Not inplace unless specified!
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
      <th>new</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
      <td>3.614819</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
      <td>-0.196959</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
      <td>-1.489355</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
      <td>-0.744542</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
      <td>2.796762</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.drop('new',axis=1,inplace=True)
```

```python
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>
</div>


Can also drop rows this way:

```python
df.drop('E',axis=0)
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
    </tr>
  </tbody>
</table>
</div>

#### Selecting Rows

```python
df.loc['A']
```

    W    2.706850
    X    0.628133
    Y    0.907969
    Z    0.503826
    Name: A, dtype: float64

Or select based off of position instead of label 

```python
df.iloc[2]
```

    W   -2.018168
    X    0.740122
    Y    0.528813
    Z   -0.589001
    Name: C, dtype: float64

#### Selecting subset of rows and columns

```python
df.loc['B','Y']
```

    -0.84807698340363147

```python
df.loc[['A','B'],['W','Y']]
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>Y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.907969</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.848077</td>
    </tr>
  </tbody>
</table>
</div>

### Conditional Selection

An important feature of pandas is conditional selection using bracket notation, very similar to numpy:

```python
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>
</div>

```python
df>0
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>B</th>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>C</th>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>D</th>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>E</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>

```python
df[df>0]
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>C</th>
      <td>NaN</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>
</div>

```python
df[df['W']>0]
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>
</div>

```python
df[df['W']>0]['Y']
```

    A    0.907969
    B   -0.848077
    D   -0.933237
    E    2.605967
    Name: Y, dtype: float64

```python
df[df['W']>0][['Y','X']]
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Y</th>
      <th>X</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>0.907969</td>
      <td>0.628133</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-0.848077</td>
      <td>-0.319318</td>
    </tr>
    <tr>
      <th>D</th>
      <td>-0.933237</td>
      <td>-0.758872</td>
    </tr>
    <tr>
      <th>E</th>
      <td>2.605967</td>
      <td>1.978757</td>
    </tr>
  </tbody>
</table>
</div>

For two conditions you can use | and & with parenthesis:

```python
df[(df['W']>0) & (df['Y'] > 1)]
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>
</div>

### More Index Details

Let's discuss some more features of indexing, including resetting the index or setting it something else. We'll also talk about index hierarchy!

```python
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>
</div>

```python
# Reset to default 0,1...n index
df.reset_index()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D</td>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>4</th>
      <td>E</td>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>
</div>

```python
newind = 'CA NY WY OR CO'.split()
```

```python
df['States'] = newind
```

```python
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
      <th>States</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
      <td>NY</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
      <td>WY</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
      <td>OR</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
      <td>CO</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.set_index('States')
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
    <tr>
      <th>States</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CA</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>NY</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>WY</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
    </tr>
    <tr>
      <th>OR</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>CO</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>
</div>

```python
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
      <th>States</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
      <td>NY</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
      <td>WY</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
      <td>OR</td>
    </tr>
    <tr>
      <th>E</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
      <td>CO</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.set_index('States',inplace=True)
```

```python
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>W</th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
    <tr>
      <th>States</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>CA</th>
      <td>2.706850</td>
      <td>0.628133</td>
      <td>0.907969</td>
      <td>0.503826</td>
    </tr>
    <tr>
      <th>NY</th>
      <td>0.651118</td>
      <td>-0.319318</td>
      <td>-0.848077</td>
      <td>0.605965</td>
    </tr>
    <tr>
      <th>WY</th>
      <td>-2.018168</td>
      <td>0.740122</td>
      <td>0.528813</td>
      <td>-0.589001</td>
    </tr>
    <tr>
      <th>OR</th>
      <td>0.188695</td>
      <td>-0.758872</td>
      <td>-0.933237</td>
      <td>0.955057</td>
    </tr>
    <tr>
      <th>CO</th>
      <td>0.190794</td>
      <td>1.978757</td>
      <td>2.605967</td>
      <td>0.683509</td>
    </tr>
  </tbody>
</table>
</div>

### Multi-Index and Index Hierarchy

Let us go over how to work with Multi-Index, first we'll create a quick example of what a Multi-Indexed DataFrame would look like:

```python
# Index Levels
outside = ['G1','G1','G1','G2','G2','G2']
inside = [1,2,3,1,2,3]
hier_index = list(zip(outside,inside))
hier_index = pd.MultiIndex.from_tuples(hier_index)
```

```python
hier_index
```

    MultiIndex(levels=[['G1', 'G2'], [1, 2, 3]],
               labels=[[0, 0, 0, 1, 1, 1], [0, 1, 2, 0, 1, 2]])

```python
df = pd.DataFrame(np.random.randn(6,2),index=hier_index,columns=['A','B'])
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">G1</th>
      <th>1</th>
      <td>0.153661</td>
      <td>0.167638</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.765930</td>
      <td>0.962299</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.902826</td>
      <td>-0.537909</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">G2</th>
      <th>1</th>
      <td>-1.549671</td>
      <td>0.435253</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.259904</td>
      <td>-0.447898</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.266207</td>
      <td>0.412580</td>
    </tr>
  </tbody>
</table>
</div>

Now let's show how to index this! For index hierarchy we use df.loc[], if this was on the columns axis, you would just use normal bracket notation df[]. Calling one level of the index returns the sub-dataframe:

```python
df.loc['G1']
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>0.153661</td>
      <td>0.167638</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.765930</td>
      <td>0.962299</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.902826</td>
      <td>-0.537909</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.loc['G1'].loc[1]
```

    A    0.153661
    B    0.167638
    Name: 1, dtype: float64

```python
df.index.names
```

    FrozenList([None, None])

```python
df.index.names = ['Group','Num']
```

```python
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>Group</th>
      <th>Num</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">G1</th>
      <th>1</th>
      <td>0.153661</td>
      <td>0.167638</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.765930</td>
      <td>0.962299</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.902826</td>
      <td>-0.537909</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">G2</th>
      <th>1</th>
      <td>-1.549671</td>
      <td>0.435253</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.259904</td>
      <td>-0.447898</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.266207</td>
      <td>0.412580</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.xs('G1')
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>Num</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>0.153661</td>
      <td>0.167638</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.765930</td>
      <td>0.962299</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.902826</td>
      <td>-0.537909</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.xs(['G1',1])
```

    A    0.153661
    B    0.167638
    Name: (G1, 1), dtype: float64

```python
df.xs(1,level='Num')
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>Group</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>G1</th>
      <td>0.153661</td>
      <td>0.167638</td>
    </tr>
    <tr>
      <th>G2</th>
      <td>-1.549671</td>
      <td>0.435253</td>
    </tr>
  </tbody>
</table>
</div>

### Missing Data

Let's show a few convenient methods to deal with Missing Data in pandas:

```python
import numpy as np
import pandas as pd
```

```python
df = pd.DataFrame({'A':[1,2,np.nan],
                  'B':[5,np.nan,np.nan],
                  'C':[1,2,3]})
```

```python
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>5.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>NaN</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.dropna()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>5.0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.dropna(axis=1)
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.dropna(thresh=2)
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>5.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>NaN</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.fillna(value='FILL VALUE')
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>5</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>FILL VALUE</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>FILL VALUE</td>
      <td>FILL VALUE</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>

```python
df['A'].fillna(value=df['A'].mean())
```

    0    1.0
    1    2.0
    2    1.5
    Name: A, dtype: float64

### Groupby

The groupby method allows you to group rows of data together and call aggregate functions

```python
import pandas as pd
# Create dataframe
data = {'Company':['GOOG','GOOG','MSFT','MSFT','FB','FB'],
       'Person':['Sam','Charlie','Amy','Vanessa','Carl','Sarah'],
       'Sales':[200,120,340,124,243,350]}
```

```python
df = pd.DataFrame(data)
```

```python
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Company</th>
      <th>Person</th>
      <th>Sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>GOOG</td>
      <td>Sam</td>
      <td>200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>GOOG</td>
      <td>Charlie</td>
      <td>120</td>
    </tr>
    <tr>
      <th>2</th>
      <td>MSFT</td>
      <td>Amy</td>
      <td>340</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MSFT</td>
      <td>Vanessa</td>
      <td>124</td>
    </tr>
    <tr>
      <th>4</th>
      <td>FB</td>
      <td>Carl</td>
      <td>243</td>
    </tr>
    <tr>
      <th>5</th>
      <td>FB</td>
      <td>Sarah</td>
      <td>350</td>
    </tr>
  </tbody>
</table>
</div>

Now you can use the .groupby() method to group rows together based off of a column name. For instance let's group based off of Company. This will create a DataFrameGroupBy object:

```python
df.groupby('Company')
```

You can save this object as a new variable:

```python
by_comp = df.groupby("Company")
```

And then call aggregate methods off the object:

```python
by_comp.mean()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Sales</th>
    </tr>
    <tr>
      <th>Company</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>FB</th>
      <td>296.5</td>
    </tr>
    <tr>
      <th>GOOG</th>
      <td>160.0</td>
    </tr>
    <tr>
      <th>MSFT</th>
      <td>232.0</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.groupby('Company').mean()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Sales</th>
    </tr>
    <tr>
      <th>Company</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>FB</th>
      <td>296.5</td>
    </tr>
    <tr>
      <th>GOOG</th>
      <td>160.0</td>
    </tr>
    <tr>
      <th>MSFT</th>
      <td>232.0</td>
    </tr>
  </tbody>
</table>
</div>

More examples of aggregate methods:

```python
by_comp.std()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Sales</th>
    </tr>
    <tr>
      <th>Company</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>FB</th>
      <td>75.660426</td>
    </tr>
    <tr>
      <th>GOOG</th>
      <td>56.568542</td>
    </tr>
    <tr>
      <th>MSFT</th>
      <td>152.735065</td>
    </tr>
  </tbody>
</table>
</div>

```python
by_comp.min()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Person</th>
      <th>Sales</th>
    </tr>
    <tr>
      <th>Company</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>FB</th>
      <td>Carl</td>
      <td>243</td>
    </tr>
    <tr>
      <th>GOOG</th>
      <td>Charlie</td>
      <td>120</td>
    </tr>
    <tr>
      <th>MSFT</th>
      <td>Amy</td>
      <td>124</td>
    </tr>
  </tbody>
</table>
</div>

```python
by_comp.max()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Person</th>
      <th>Sales</th>
    </tr>
    <tr>
      <th>Company</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>FB</th>
      <td>Sarah</td>
      <td>350</td>
    </tr>
    <tr>
      <th>GOOG</th>
      <td>Sam</td>
      <td>200</td>
    </tr>
    <tr>
      <th>MSFT</th>
      <td>Vanessa</td>
      <td>340</td>
    </tr>
  </tbody>
</table>
</div>

```python
by_comp.count()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Person</th>
      <th>Sales</th>
    </tr>
    <tr>
      <th>Company</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>FB</th>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>GOOG</th>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>MSFT</th>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>

```python
by_comp.describe()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Sales</th>
    </tr>
    <tr>
      <th>Company</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="8" valign="top">FB</th>
      <th>count</th>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>296.500000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>75.660426</td>
    </tr>
    <tr>
      <th>min</th>
      <td>243.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>269.750000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>296.500000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>323.250000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>350.000000</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">GOOG</th>
      <th>count</th>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>160.000000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>56.568542</td>
    </tr>
    <tr>
      <th>min</th>
      <td>120.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>140.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>160.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>180.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>200.000000</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">MSFT</th>
      <th>count</th>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>232.000000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>152.735065</td>
    </tr>
    <tr>
      <th>min</th>
      <td>124.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>178.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>232.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>286.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>340.000000</td>
    </tr>
  </tbody>
</table>
</div>

```python
by_comp.describe().transpose()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Company</th>
      <th colspan="8" halign="left">FB</th>
      <th colspan="5" halign="left">GOOG</th>
      <th colspan="8" halign="left">MSFT</th>
    </tr>
    <tr>
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
      <th>count</th>
      <th>mean</th>
      <th>...</th>
      <th>75%</th>
      <th>max</th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Sales</th>
      <td>2.0</td>
      <td>296.5</td>
      <td>75.660426</td>
      <td>243.0</td>
      <td>269.75</td>
      <td>296.5</td>
      <td>323.25</td>
      <td>350.0</td>
      <td>2.0</td>
      <td>160.0</td>
      <td>...</td>
      <td>180.0</td>
      <td>200.0</td>
      <td>2.0</td>
      <td>232.0</td>
      <td>152.735065</td>
      <td>124.0</td>
      <td>178.0</td>
      <td>232.0</td>
      <td>286.0</td>
      <td>340.0</td>
    </tr>
  </tbody>
</table>
<p>1 rows × 24 columns</p>
</div>

```python
by_comp.describe().transpose()['GOOG']
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Sales</th>
      <td>2.0</td>
      <td>160.0</td>
      <td>56.568542</td>
      <td>120.0</td>
      <td>140.0</td>
      <td>160.0</td>
      <td>180.0</td>
      <td>200.0</td>
    </tr>
  </tbody>
</table>
</div>

### Merging, Joining, and Concatenating

There are 3 main ways of combining DataFrames together: Merging, Joining and Concatenating. In this lecture we will discuss these 3 methods with examples.

#### Example DataFrames

```python
import pandas as pd
```

```python
df1 = pd.DataFrame({'A': ['A0', 'A1', 'A2', 'A3'],
                        'B': ['B0', 'B1', 'B2', 'B3'],
                        'C': ['C0', 'C1', 'C2', 'C3'],
                        'D': ['D0', 'D1', 'D2', 'D3']},
                        index=[0, 1, 2, 3])
```

```python
df2 = pd.DataFrame({'A': ['A4', 'A5', 'A6', 'A7'],
                        'B': ['B4', 'B5', 'B6', 'B7'],
                        'C': ['C4', 'C5', 'C6', 'C7'],
                        'D': ['D4', 'D5', 'D6', 'D7']},
                         index=[4, 5, 6, 7]) 
```

```python
df3 = pd.DataFrame({'A': ['A8', 'A9', 'A10', 'A11'],
                        'B': ['B8', 'B9', 'B10', 'B11'],
                        'C': ['C8', 'C9', 'C10', 'C11'],
                        'D': ['D8', 'D9', 'D10', 'D11']},
                        index=[8, 9, 10, 11])
```

```python
df1
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0</td>
      <td>B0</td>
      <td>C0</td>
      <td>D0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A1</td>
      <td>B1</td>
      <td>C1</td>
      <td>D1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A2</td>
      <td>B2</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A3</td>
      <td>B3</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
  </tbody>
</table>
</div>

```python
df2
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>A4</td>
      <td>B4</td>
      <td>C4</td>
      <td>D4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>A5</td>
      <td>B5</td>
      <td>C5</td>
      <td>D5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>A6</td>
      <td>B6</td>
      <td>C6</td>
      <td>D6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>A7</td>
      <td>B7</td>
      <td>C7</td>
      <td>D7</td>
    </tr>
  </tbody>
</table>
</div>

```python
df3
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8</th>
      <td>A8</td>
      <td>B8</td>
      <td>C8</td>
      <td>D8</td>
    </tr>
    <tr>
      <th>9</th>
      <td>A9</td>
      <td>B9</td>
      <td>C9</td>
      <td>D9</td>
    </tr>
    <tr>
      <th>10</th>
      <td>A10</td>
      <td>B10</td>
      <td>C10</td>
      <td>D10</td>
    </tr>
    <tr>
      <th>11</th>
      <td>A11</td>
      <td>B11</td>
      <td>C11</td>
      <td>D11</td>
    </tr>
  </tbody>
</table>
</div>

### Concatenation

Concatenation basically glues together DataFrames. Keep in mind that dimensions should match along the axis you are concatenating on. You can use **pd.concat** and pass in a list of DataFrames to concatenate together:

```python
pd.concat([df1,df2,df3])
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0</td>
      <td>B0</td>
      <td>C0</td>
      <td>D0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A1</td>
      <td>B1</td>
      <td>C1</td>
      <td>D1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A2</td>
      <td>B2</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A3</td>
      <td>B3</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A4</td>
      <td>B4</td>
      <td>C4</td>
      <td>D4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>A5</td>
      <td>B5</td>
      <td>C5</td>
      <td>D5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>A6</td>
      <td>B6</td>
      <td>C6</td>
      <td>D6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>A7</td>
      <td>B7</td>
      <td>C7</td>
      <td>D7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>A8</td>
      <td>B8</td>
      <td>C8</td>
      <td>D8</td>
    </tr>
    <tr>
      <th>9</th>
      <td>A9</td>
      <td>B9</td>
      <td>C9</td>
      <td>D9</td>
    </tr>
    <tr>
      <th>10</th>
      <td>A10</td>
      <td>B10</td>
      <td>C10</td>
      <td>D10</td>
    </tr>
    <tr>
      <th>11</th>
      <td>A11</td>
      <td>B11</td>
      <td>C11</td>
      <td>D11</td>
    </tr>
  </tbody>
</table>
</div>

```python
pd.concat([df1,df2,df3],axis=1)
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0</td>
      <td>B0</td>
      <td>C0</td>
      <td>D0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A1</td>
      <td>B1</td>
      <td>C1</td>
      <td>D1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A2</td>
      <td>B2</td>
      <td>C2</td>
      <td>D2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A3</td>
      <td>B3</td>
      <td>C3</td>
      <td>D3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A4</td>
      <td>B4</td>
      <td>C4</td>
      <td>D4</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A5</td>
      <td>B5</td>
      <td>C5</td>
      <td>D5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A6</td>
      <td>B6</td>
      <td>C6</td>
      <td>D6</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A7</td>
      <td>B7</td>
      <td>C7</td>
      <td>D7</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A8</td>
      <td>B8</td>
      <td>C8</td>
      <td>D8</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A9</td>
      <td>B9</td>
      <td>C9</td>
      <td>D9</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A10</td>
      <td>B10</td>
      <td>C10</td>
      <td>D10</td>
    </tr>
    <tr>
      <th>11</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A11</td>
      <td>B11</td>
      <td>C11</td>
      <td>D11</td>
    </tr>
  </tbody>
</table>
</div>

#### Example DataFrames

```python
left = pd.DataFrame({'key': ['K0', 'K1', 'K2', 'K3'],
                     'A': ['A0', 'A1', 'A2', 'A3'],
                     'B': ['B0', 'B1', 'B2', 'B3']})
   
right = pd.DataFrame({'key': ['K0', 'K1', 'K2', 'K3'],
                          'C': ['C0', 'C1', 'C2', 'C3'],
                          'D': ['D0', 'D1', 'D2', 'D3']})    
```

```python
left
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>key</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0</td>
      <td>B0</td>
      <td>K0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A1</td>
      <td>B1</td>
      <td>K1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A2</td>
      <td>B2</td>
      <td>K2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A3</td>
      <td>B3</td>
      <td>K3</td>
    </tr>
  </tbody>
</table>
</div>

```python
right
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>C</th>
      <th>D</th>
      <th>key</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>C0</td>
      <td>D0</td>
      <td>K0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C1</td>
      <td>D1</td>
      <td>K1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C2</td>
      <td>D2</td>
      <td>K2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>C3</td>
      <td>D3</td>
      <td>K3</td>
    </tr>
  </tbody>
</table>
</div>

### Merging

The **merge** function allows you to merge DataFrames together using a similar logic as merging SQL Tables together. For example:

```python
pd.merge(left,right,how='inner',on='key')
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>key</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0</td>
      <td>B0</td>
      <td>K0</td>
      <td>C0</td>
      <td>D0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A1</td>
      <td>B1</td>
      <td>K1</td>
      <td>C1</td>
      <td>D1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A2</td>
      <td>B2</td>
      <td>K2</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A3</td>
      <td>B3</td>
      <td>K3</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
  </tbody>
</table>
</div>

Or to show a more complicated example:

```python
left = pd.DataFrame({'key1': ['K0', 'K0', 'K1', 'K2'],
                     'key2': ['K0', 'K1', 'K0', 'K1'],
                        'A': ['A0', 'A1', 'A2', 'A3'],
                        'B': ['B0', 'B1', 'B2', 'B3']})
    
right = pd.DataFrame({'key1': ['K0', 'K1', 'K1', 'K2'],
                               'key2': ['K0', 'K0', 'K0', 'K0'],
                                  'C': ['C0', 'C1', 'C2', 'C3'],
                                  'D': ['D0', 'D1', 'D2', 'D3']})
```

```python
pd.merge(left, right, on=['key1', 'key2'])
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>key1</th>
      <th>key2</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0</td>
      <td>B0</td>
      <td>K0</td>
      <td>K0</td>
      <td>C0</td>
      <td>D0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A2</td>
      <td>B2</td>
      <td>K1</td>
      <td>K0</td>
      <td>C1</td>
      <td>D1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A2</td>
      <td>B2</td>
      <td>K1</td>
      <td>K0</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
  </tbody>
</table>
</div>

```python
pd.merge(left, right, how='outer', on=['key1', 'key2'])
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>key1</th>
      <th>key2</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0</td>
      <td>B0</td>
      <td>K0</td>
      <td>K0</td>
      <td>C0</td>
      <td>D0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A1</td>
      <td>B1</td>
      <td>K0</td>
      <td>K1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A2</td>
      <td>B2</td>
      <td>K1</td>
      <td>K0</td>
      <td>C1</td>
      <td>D1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A2</td>
      <td>B2</td>
      <td>K1</td>
      <td>K0</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A3</td>
      <td>B3</td>
      <td>K2</td>
      <td>K1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>K2</td>
      <td>K0</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
  </tbody>
</table>
</div>

```python
pd.merge(left, right, how='right', on=['key1', 'key2'])
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>key1</th>
      <th>key2</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0</td>
      <td>B0</td>
      <td>K0</td>
      <td>K0</td>
      <td>C0</td>
      <td>D0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A2</td>
      <td>B2</td>
      <td>K1</td>
      <td>K0</td>
      <td>C1</td>
      <td>D1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A2</td>
      <td>B2</td>
      <td>K1</td>
      <td>K0</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>K2</td>
      <td>K0</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
  </tbody>
</table>
</div>

```python
pd.merge(left, right, how='left', on=['key1', 'key2'])
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>key1</th>
      <th>key2</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0</td>
      <td>B0</td>
      <td>K0</td>
      <td>K0</td>
      <td>C0</td>
      <td>D0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A1</td>
      <td>B1</td>
      <td>K0</td>
      <td>K1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A2</td>
      <td>B2</td>
      <td>K1</td>
      <td>K0</td>
      <td>C1</td>
      <td>D1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A2</td>
      <td>B2</td>
      <td>K1</td>
      <td>K0</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A3</td>
      <td>B3</td>
      <td>K2</td>
      <td>K1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

### Joining
Joining is a convenient method for combining the columns of two potentially differently-indexed DataFrames into a single result DataFrame.

```python
left = pd.DataFrame({'A': ['A0', 'A1', 'A2'],
                     'B': ['B0', 'B1', 'B2']},
                      index=['K0', 'K1', 'K2']) 

right = pd.DataFrame({'C': ['C0', 'C2', 'C3'],
                    'D': ['D0', 'D2', 'D3']},
                      index=['K0', 'K2', 'K3'])
```

```python
left.join(right)
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>K0</th>
      <td>A0</td>
      <td>B0</td>
      <td>C0</td>
      <td>D0</td>
    </tr>
    <tr>
      <th>K1</th>
      <td>A1</td>
      <td>B1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>K2</th>
      <td>A2</td>
      <td>B2</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
  </tbody>
</table>
</div>

```python
left.join(right, how='outer')
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>K0</th>
      <td>A0</td>
      <td>B0</td>
      <td>C0</td>
      <td>D0</td>
    </tr>
    <tr>
      <th>K1</th>
      <td>A1</td>
      <td>B1</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>K2</th>
      <td>A2</td>
      <td>B2</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>K3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
  </tbody>
</table>
</div>

## Operations

There are lots of operations with pandas that will be really useful to you, but don't fall into any distinct category. Let's show them here in this lecture:

```python
import pandas as pd
df = pd.DataFrame({'col1':[1,2,3,4],'col2':[444,555,666,444],'col3':['abc','def','ghi','xyz']})
df.head()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>444</td>
      <td>abc</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>555</td>
      <td>def</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>666</td>
      <td>ghi</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>444</td>
      <td>xyz</td>
    </tr>
  </tbody>
</table>
</div>

### Info on Unique Values

```python
df['col2'].unique()
```

    array([444, 555, 666])

```python
df['col2'].nunique()
```

    3

```python
df['col2'].value_counts()
```

    444    2
    555    1
    666    1
    Name: col2, dtype: int64

### Selecting Data

```python
#Select from DataFrame using criteria from multiple columns
newdf = df[(df['col1']>2) & (df['col2']==444)]
```

```python
newdf
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>444</td>
      <td>xyz</td>
    </tr>
  </tbody>
</table>
</div>

### Applying Functions

```python
def times2(x):
    return x*2
```

```python
df['col1'].apply(times2)
```

    0    2
    1    4
    2    6
    3    8
    Name: col1, dtype: int64

```python
df['col3'].apply(len)
```

    0    3
    1    3
    2    3
    3    3
    Name: col3, dtype: int64

```python
df['col1'].sum()
```

    10

### Permanently Removing a Column

```python
del df['col1']
```

```python
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>444</td>
      <td>abc</td>
    </tr>
    <tr>
      <th>1</th>
      <td>555</td>
      <td>def</td>
    </tr>
    <tr>
      <th>2</th>
      <td>666</td>
      <td>ghi</td>
    </tr>
    <tr>
      <th>3</th>
      <td>444</td>
      <td>xyz</td>
    </tr>
  </tbody>
</table>
</div>

### Get column and index names

```python
df.columns
```

    Index(['col2', 'col3'], dtype='object')

```python
df.index
```

    RangeIndex(start=0, stop=4, step=1)

### Sorting and Ordering a DataFrame

```python
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>444</td>
      <td>abc</td>
    </tr>
    <tr>
      <th>1</th>
      <td>555</td>
      <td>def</td>
    </tr>
    <tr>
      <th>2</th>
      <td>666</td>
      <td>ghi</td>
    </tr>
    <tr>
      <th>3</th>
      <td>444</td>
      <td>xyz</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.sort_values(by='col2') #inplace=False by default
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>444</td>
      <td>abc</td>
    </tr>
    <tr>
      <th>3</th>
      <td>444</td>
      <td>xyz</td>
    </tr>
    <tr>
      <th>1</th>
      <td>555</td>
      <td>def</td>
    </tr>
    <tr>
      <th>2</th>
      <td>666</td>
      <td>ghi</td>
    </tr>
  </tbody>
</table>
</div>

### Find Null Values or Check for Null Values

```python
df.isnull()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>

```python
# Drop rows with NaN Values
df.dropna()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>444</td>
      <td>abc</td>
    </tr>
    <tr>
      <th>1</th>
      <td>555</td>
      <td>def</td>
    </tr>
    <tr>
      <th>2</th>
      <td>666</td>
      <td>ghi</td>
    </tr>
    <tr>
      <th>3</th>
      <td>444</td>
      <td>xyz</td>
    </tr>
  </tbody>
</table>
</div>

### Filling in NaN values with something else

```python
import numpy as np
```

```python
df = pd.DataFrame({'col1':[1,2,3,np.nan],
                   'col2':[np.nan,555,666,444],
                   'col3':['abc','def','ghi','xyz']})
df.head()
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>abc</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>555.0</td>
      <td>def</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.0</td>
      <td>666.0</td>
      <td>ghi</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>444.0</td>
      <td>xyz</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.fillna('FILL')
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>col1</th>
      <th>col2</th>
      <th>col3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>FILL</td>
      <td>abc</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>555</td>
      <td>def</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>666</td>
      <td>ghi</td>
    </tr>
    <tr>
      <th>3</th>
      <td>FILL</td>
      <td>444</td>
      <td>xyz</td>
    </tr>
  </tbody>
</table>
</div>

```python
data = {'A':['foo','foo','foo','bar','bar','bar'],
     'B':['one','one','two','two','one','one'],
       'C':['x','y','x','y','x','y'],
       'D':[1,3,2,5,4,1]}

df = pd.DataFrame(data)
```

```python
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>one</td>
      <td>x</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>one</td>
      <td>y</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foo</td>
      <td>two</td>
      <td>x</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>bar</td>
      <td>two</td>
      <td>y</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>bar</td>
      <td>one</td>
      <td>x</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>bar</td>
      <td>one</td>
      <td>y</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.pivot_table(values='D',index=['A', 'B'],columns=['C'])
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>C</th>
      <th>x</th>
      <th>y</th>
    </tr>
    <tr>
      <th>A</th>
      <th>B</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>one</th>
      <td>4.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>two</th>
      <td>NaN</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">foo</th>
      <th>one</th>
      <td>1.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

## CSV Data

### CSV Input

```python
df = pd.read_csv('example')
df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>

### CSV Output

```python
df.to_csv('example',index=False)
```

## Excel Data

Pandas can read and write excel files, keep in mind, this only imports data. Not formulas or images, having images or macros may cause this read_excel method to crash. 

### Excel Input

```python
pd.read_excel('Excel_Sample.xlsx',sheetname='Sheet1')
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>

### Excel Output

```python
df.to_excel('Excel_Sample.xlsx',sheet_name='Sheet1')
```

## HTML Data

You may need to install htmllib5,lxml, and BeautifulSoup4. In your terminal/command prompt run:

    conda install lxml
    conda install html5lib
    conda install BeautifulSoup4

Then restart Jupyter Notebook.
(or use pip install if you aren't using the Anaconda Distribution)

Pandas can read table tabs off of html. For example:

### HTML Input

Pandas read_html function will read tables off of a webpage and return a list of DataFrame objects:

```python
df = pd.read_html('http://www.fdic.gov/bank/individual/failed/banklist.html')
```

```python
df[0]
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Bank Name</th>
      <th>City</th>
      <th>ST</th>
      <th>CERT</th>
      <th>Acquiring Institution</th>
      <th>Closing Date</th>
      <th>Updated Date</th>
      <th>Loss Share Type</th>
      <th>Agreement Terminated</th>
      <th>Termination Date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>First CornerStone Bank</td>
      <td>King of Prussia</td>
      <td>PA</td>
      <td>35312</td>
      <td>First-Citizens Bank &amp; Trust Company</td>
      <td>May 6, 2016</td>
      <td>July 12, 2016</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Trust Company Bank</td>
      <td>Memphis</td>
      <td>TN</td>
      <td>9956</td>
      <td>The Bank of Fayette County</td>
      <td>April 29, 2016</td>
      <td>August 4, 2016</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>North Milwaukee State Bank</td>
      <td>Milwaukee</td>
      <td>WI</td>
      <td>20364</td>
      <td>First-Citizens Bank &amp; Trust Company</td>
      <td>March 11, 2016</td>
      <td>June 16, 2016</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hometown National Bank</td>
      <td>Longview</td>
      <td>WA</td>
      <td>35156</td>
      <td>Twin City Bank</td>
      <td>October 2, 2015</td>
      <td>April 13, 2016</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>The Bank of Georgia</td>
      <td>Peachtree City</td>
      <td>GA</td>
      <td>35259</td>
      <td>Fidelity Bank</td>
      <td>October 2, 2015</td>
      <td>April 13, 2016</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Premier Bank</td>
      <td>Denver</td>
      <td>CO</td>
      <td>34112</td>
      <td>United Fidelity Bank, fsb</td>
      <td>July 10, 2015</td>
      <td>July 12, 2016</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Edgebrook Bank</td>
      <td>Chicago</td>
      <td>IL</td>
      <td>57772</td>
      <td>Republic Bank of Chicago</td>
      <td>May 8, 2015</td>
      <td>July 12, 2016</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Doral BankEn Espanol</td>
      <td>San Juan</td>
      <td>PR</td>
      <td>32102</td>
      <td>Banco Popular de Puerto Rico</td>
      <td>February 27, 2015</td>
      <td>May 13, 2015</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Capitol City Bank &amp; Trust Company</td>
      <td>Atlanta</td>
      <td>GA</td>
      <td>33938</td>
      <td>First-Citizens Bank &amp; Trust Company</td>
      <td>February 13, 2015</td>
      <td>April 21, 2015</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Highland Community Bank</td>
      <td>Chicago</td>
      <td>IL</td>
      <td>20290</td>
      <td>United Fidelity Bank, fsb</td>
      <td>January 23, 2015</td>
      <td>April 21, 2015</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>First National Bank of Crestview</td>
      <td>Crestview</td>
      <td>FL</td>
      <td>17557</td>
      <td>First NBC Bank</td>
      <td>January 16, 2015</td>
      <td>January 15, 2016</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Northern Star Bank</td>
      <td>Mankato</td>
      <td>MN</td>
      <td>34983</td>
      <td>BankVista</td>
      <td>December 19, 2014</td>
      <td>January 6, 2016</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Frontier Bank, FSB D/B/A El Paseo Bank</td>
      <td>Palm Desert</td>
      <td>CA</td>
      <td>34738</td>
      <td>Bank of Southern California, N.A.</td>
      <td>November 7, 2014</td>
      <td>January 6, 2016</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>13</th>
      <td>The National Republic Bank of Chicago</td>
      <td>Chicago</td>
      <td>IL</td>
      <td>916</td>
      <td>State Bank of Texas</td>
      <td>October 24, 2014</td>
      <td>January 6, 2016</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>14</th>
      <td>NBRS Financial</td>
      <td>Rising Sun</td>
      <td>MD</td>
      <td>4862</td>
      <td>Howard Bank</td>
      <td>October 17, 2014</td>
      <td>March 26, 2015</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15</th>
      <td>GreenChoice Bank, fsb</td>
      <td>Chicago</td>
      <td>IL</td>
      <td>28462</td>
      <td>Providence Bank, LLC</td>
      <td>July 25, 2014</td>
      <td>July 28, 2015</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Eastside Commercial Bank</td>
      <td>Conyers</td>
      <td>GA</td>
      <td>58125</td>
      <td>Community &amp; Southern Bank</td>
      <td>July 18, 2014</td>
      <td>July 11, 2016</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>17</th>
      <td>The Freedom State Bank</td>
      <td>Freedom</td>
      <td>OK</td>
      <td>12483</td>
      <td>Alva State Bank &amp; Trust Company</td>
      <td>June 27, 2014</td>
      <td>March 25, 2016</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Valley Bank</td>
      <td>Fort Lauderdale</td>
      <td>FL</td>
      <td>21793</td>
      <td>Landmark Bank, National Association</td>
      <td>June 20, 2014</td>
      <td>June 29, 2015</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Valley Bank</td>
      <td>Moline</td>
      <td>IL</td>
      <td>10450</td>
      <td>Great Southern Bank</td>
      <td>June 20, 2014</td>
      <td>June 26, 2015</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Slavie Federal Savings Bank</td>
      <td>Bel Air</td>
      <td>MD</td>
      <td>32368</td>
      <td>Bay Bank, FSB</td>
      <td>May 30, 2014</td>
      <td>June 15, 2015</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Columbia Savings Bank</td>
      <td>Cincinnati</td>
      <td>OH</td>
      <td>32284</td>
      <td>United Fidelity Bank, fsb</td>
      <td>May 23, 2014</td>
      <td>May 28, 2015</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>22</th>
      <td>AztecAmerica Bank En Espanol</td>
      <td>Berwyn</td>
      <td>IL</td>
      <td>57866</td>
      <td>Republic Bank of Chicago</td>
      <td>May 16, 2014</td>
      <td>July 18, 2014</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Allendale County Bank</td>
      <td>Fairfax</td>
      <td>SC</td>
      <td>15062</td>
      <td>Palmetto State Bank</td>
      <td>April 25, 2014</td>
      <td>July 18, 2014</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Vantage Point Bank</td>
      <td>Horsham</td>
      <td>PA</td>
      <td>58531</td>
      <td>First Choice Bank</td>
      <td>February 28, 2014</td>
      <td>March 3, 2015</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Millennium Bank, National Association</td>
      <td>Sterling</td>
      <td>VA</td>
      <td>35096</td>
      <td>WashingtonFirst Bank</td>
      <td>February 28, 2014</td>
      <td>March 03, 2015</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Syringa Bank</td>
      <td>Boise</td>
      <td>ID</td>
      <td>34296</td>
      <td>Sunwest Bank</td>
      <td>January 31, 2014</td>
      <td>April 12, 2016</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>27</th>
      <td>The Bank of Union</td>
      <td>El Reno</td>
      <td>OK</td>
      <td>17967</td>
      <td>BancFirst</td>
      <td>January 24, 2014</td>
      <td>March 25, 2016</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>28</th>
      <td>DuPage National Bank</td>
      <td>West Chicago</td>
      <td>IL</td>
      <td>5732</td>
      <td>Republic Bank of Chicago</td>
      <td>January 17, 2014</td>
      <td>February 19, 2015</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Texas Community Bank, National Association</td>
      <td>The Woodlands</td>
      <td>TX</td>
      <td>57431</td>
      <td>Spirit of Texas Bank, SSB</td>
      <td>December 13, 2013</td>
      <td>December 29, 2014</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>515</th>
      <td>ANB Financial, NA</td>
      <td>Bentonville</td>
      <td>AR</td>
      <td>33901</td>
      <td>Pulaski Bank and Trust Company</td>
      <td>May 9, 2008</td>
      <td>August 28, 2012</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>516</th>
      <td>Hume Bank</td>
      <td>Hume</td>
      <td>MO</td>
      <td>1971</td>
      <td>Security Bank</td>
      <td>March 7, 2008</td>
      <td>August 28, 2012</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>517</th>
      <td>Douglass National Bank</td>
      <td>Kansas City</td>
      <td>MO</td>
      <td>24660</td>
      <td>Liberty Bank and Trust Company</td>
      <td>January 25, 2008</td>
      <td>October 26, 2012</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>518</th>
      <td>Miami Valley Bank</td>
      <td>Lakeview</td>
      <td>OH</td>
      <td>16848</td>
      <td>The Citizens Banking Company</td>
      <td>October 4, 2007</td>
      <td>August 28, 2012</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>519</th>
      <td>NetBank</td>
      <td>Alpharetta</td>
      <td>GA</td>
      <td>32575</td>
      <td>ING DIRECT</td>
      <td>September 28, 2007</td>
      <td>August 28, 2012</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>520</th>
      <td>Metropolitan Savings Bank</td>
      <td>Pittsburgh</td>
      <td>PA</td>
      <td>35353</td>
      <td>Allegheny Valley Bank of Pittsburgh</td>
      <td>February 2, 2007</td>
      <td>October 27, 2010</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>521</th>
      <td>Bank of Ephraim</td>
      <td>Ephraim</td>
      <td>UT</td>
      <td>1249</td>
      <td>Far West Bank</td>
      <td>June 25, 2004</td>
      <td>April 9, 2008</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>522</th>
      <td>Reliance Bank</td>
      <td>White Plains</td>
      <td>NY</td>
      <td>26778</td>
      <td>Union State Bank</td>
      <td>March 19, 2004</td>
      <td>April 9, 2008</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>523</th>
      <td>Guaranty National Bank of Tallahassee</td>
      <td>Tallahassee</td>
      <td>FL</td>
      <td>26838</td>
      <td>Hancock Bank of Florida</td>
      <td>March 12, 2004</td>
      <td>June 5, 2012</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>524</th>
      <td>Dollar Savings Bank</td>
      <td>Newark</td>
      <td>NJ</td>
      <td>31330</td>
      <td>No Acquirer</td>
      <td>February 14, 2004</td>
      <td>April 9, 2008</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>525</th>
      <td>Pulaski Savings Bank</td>
      <td>Philadelphia</td>
      <td>PA</td>
      <td>27203</td>
      <td>Earthstar Bank</td>
      <td>November 14, 2003</td>
      <td>July 22, 2005</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>526</th>
      <td>First National Bank of Blanchardville</td>
      <td>Blanchardville</td>
      <td>WI</td>
      <td>11639</td>
      <td>The Park Bank</td>
      <td>May 9, 2003</td>
      <td>June 5, 2012</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>527</th>
      <td>Southern Pacific Bank</td>
      <td>Torrance</td>
      <td>CA</td>
      <td>27094</td>
      <td>Beal Bank</td>
      <td>February 7, 2003</td>
      <td>October 20, 2008</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>528</th>
      <td>Farmers Bank of Cheneyville</td>
      <td>Cheneyville</td>
      <td>LA</td>
      <td>16445</td>
      <td>Sabine State Bank &amp; Trust</td>
      <td>December 17, 2002</td>
      <td>October 20, 2004</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>529</th>
      <td>Bank of Alamo</td>
      <td>Alamo</td>
      <td>TN</td>
      <td>9961</td>
      <td>No Acquirer</td>
      <td>November 8, 2002</td>
      <td>March 18, 2005</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>530</th>
      <td>AmTrade International BankEn Espanol</td>
      <td>Atlanta</td>
      <td>GA</td>
      <td>33784</td>
      <td>No Acquirer</td>
      <td>September 30, 2002</td>
      <td>September 11, 2006</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>531</th>
      <td>Universal Federal Savings Bank</td>
      <td>Chicago</td>
      <td>IL</td>
      <td>29355</td>
      <td>Chicago Community Bank</td>
      <td>June 27, 2002</td>
      <td>April 9, 2008</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>532</th>
      <td>Connecticut Bank of Commerce</td>
      <td>Stamford</td>
      <td>CT</td>
      <td>19183</td>
      <td>Hudson United Bank</td>
      <td>June 26, 2002</td>
      <td>February 14, 2012</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>533</th>
      <td>New Century Bank</td>
      <td>Shelby Township</td>
      <td>MI</td>
      <td>34979</td>
      <td>No Acquirer</td>
      <td>March 28, 2002</td>
      <td>March 18, 2005</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>534</th>
      <td>Net 1st National Bank</td>
      <td>Boca Raton</td>
      <td>FL</td>
      <td>26652</td>
      <td>Bank Leumi USA</td>
      <td>March 1, 2002</td>
      <td>April 9, 2008</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>535</th>
      <td>NextBank, NA</td>
      <td>Phoenix</td>
      <td>AZ</td>
      <td>22314</td>
      <td>No Acquirer</td>
      <td>February 7, 2002</td>
      <td>February 5, 2015</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>536</th>
      <td>Oakwood Deposit Bank Co.</td>
      <td>Oakwood</td>
      <td>OH</td>
      <td>8966</td>
      <td>The State Bank &amp; Trust Company</td>
      <td>February 1, 2002</td>
      <td>October 25, 2012</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>537</th>
      <td>Bank of Sierra Blanca</td>
      <td>Sierra Blanca</td>
      <td>TX</td>
      <td>22002</td>
      <td>The Security State Bank of Pecos</td>
      <td>January 18, 2002</td>
      <td>November 6, 2003</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>538</th>
      <td>Hamilton Bank, NAEn Espanol</td>
      <td>Miami</td>
      <td>FL</td>
      <td>24382</td>
      <td>Israel Discount Bank of New York</td>
      <td>January 11, 2002</td>
      <td>September 21, 2015</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>539</th>
      <td>Sinclair National Bank</td>
      <td>Gravette</td>
      <td>AR</td>
      <td>34248</td>
      <td>Delta Trust &amp; Bank</td>
      <td>September 7, 2001</td>
      <td>February 10, 2004</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>540</th>
      <td>Superior Bank, FSB</td>
      <td>Hinsdale</td>
      <td>IL</td>
      <td>32646</td>
      <td>Superior Federal, FSB</td>
      <td>July 27, 2001</td>
      <td>August 19, 2014</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>541</th>
      <td>Malta National Bank</td>
      <td>Malta</td>
      <td>OH</td>
      <td>6629</td>
      <td>North Valley Bank</td>
      <td>May 3, 2001</td>
      <td>November 18, 2002</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>542</th>
      <td>First Alliance Bank &amp; Trust Co.</td>
      <td>Manchester</td>
      <td>NH</td>
      <td>34264</td>
      <td>Southern New Hampshire Bank &amp; Trust</td>
      <td>February 2, 2001</td>
      <td>February 18, 2003</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>543</th>
      <td>National State Bank of Metropolis</td>
      <td>Metropolis</td>
      <td>IL</td>
      <td>3815</td>
      <td>Banterra Bank of Marion</td>
      <td>December 14, 2000</td>
      <td>March 17, 2005</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>544</th>
      <td>Bank of Honolulu</td>
      <td>Honolulu</td>
      <td>HI</td>
      <td>21029</td>
      <td>Bank of the Orient</td>
      <td>October 13, 2000</td>
      <td>March 17, 2005</td>
      <td>none</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>545 rows × 10 columns</p>
</div>

# SQL Data

* Note: If you are completely unfamiliar with SQL you can check out my other course: "Complete SQL Bootcamp" to learn SQL.

The pandas.io.sql module provides a collection of query wrappers to both facilitate data retrieval and to reduce dependency on DB-specific API. Database abstraction is provided by SQLAlchemy if installed. In addition you will need a driver library for your database. Examples of such drivers are psycopg2 for PostgreSQL or pymysql for MySQL. For SQLite this is included in Python’s standard library by default. You can find an overview of supported drivers for each SQL dialect in the SQLAlchemy docs.

If SQLAlchemy is not installed, a fallback is only provided for sqlite (and for mysql for backwards compatibility, but this is deprecated and will be removed in a future version). This mode requires a Python database adapter which respect the Python DB-API.

See also some cookbook examples for some advanced strategies.

The key functions are:

* read_sql_table(table_name, con[, schema, ...])	
    * Read SQL database table into a DataFrame.
* read_sql_query(sql, con[, index_col, ...])	
    * Read SQL query into a DataFrame.
* read_sql(sql, con[, index_col, ...])	
    * Read SQL query or database table into a DataFrame.
* DataFrame.to_sql(name, con[, flavor, ...])	
    * Write records stored in a DataFrame to a SQL database.

```python
from sqlalchemy import create_engine
```

```python
engine = create_engine('sqlite:///:memory:')
```

```python
df.to_sql('data', engine)
```

```python
sql_df = pd.read_sql('data',con=engine)
```

```python
sql_df
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>
