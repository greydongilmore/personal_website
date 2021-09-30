---
title: Data Loading
linktitle: Data Loading
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ml_intro:
    parent: 03. Data Pre-processing
    weight: 2

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

To learn how to do machine learning we're going to need some data to work with. To facilitate learning and experimentation, scikit-learn includes a <a href="https://scikit-learn.org/stable/datasets/index.html" target="_blank">datasets</a> module containing a number of widely-used toy datasets. Here's how we could load the (in)famous <a href="https://en.wikipedia.org/wiki/Iris_flower_data_set" target="_blank">Iris dataset</a>:


```python
from sklearn import datasets

# Load a dictionary (technically, a Bunch) containing the data
iris = datasets.load_iris()

# 'data' and 'target' contains the feature data and classes, respectively
X, y = iris['data'], iris['target']
```

`X` contains feature information for 150 individual Iris flowers drawn from 3 different species. `y` contains the true class information for all flowers. If we want to inspect the features in a tabular form, we can easily load the data into a pandas `DataFrame`:


```python
# Here we're importing the pandas package, which we'll use extensively
# for data manipulation. In future sections, we'll put the core imports
# at the top of the notebook, which is the convention in Python.
import pandas as pd

# Initialize a new pandas DataFrame from the X matrix and the feature names
data = pd.DataFrame(X, columns=iris['feature_names'])
data.head()
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
      <th>sepal length (cm)</th>
      <th>sepal width (cm)</th>
      <th>petal length (cm)</th>
      <th>petal width (cm)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
    </tr>
  </tbody>
</table>
</div>



In principle, we could use the iris dataset (or one of the other datasets bundled with scikit-learn) for many of the examples we'll work through. But the iris dataset has some limitations—most notably, it's fairly small (only 150 rows and 4 features), and has nothing to do with real world applications. Instead, we'll use data that should be of interest to many individuals: house pricing dataset and time-series stock prices. The housing price dataset consists of various house features along with the sales price of the home. The time-series stock price datasets will be harvested from Yahoo finance. 

We will first make use of the house pricing dataset to learn the basics of machine learning. We'll use <a href="https://pandas.pydata.org/" target="_blank">pandas</a>—the reference data analysis library in Python—to do this. Pandas provides us with a fairly magical `read_csv` function that can read in almost any kind of tabular data.


```python
# read_csv is a workhorse function that can read almost any kind of
# plain-text format. The returned object is a pandas DataFrame.

all_data = pd.read_csv('data/house_prices.csv', sep=',', index_col=0).reset_index(drop=True)
```

## Representing the data

Once the data have been read in, we can take a look at the first few rows:


```python
# head() display the first few rows of the dataset.
all_data.head()
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
      <th>MSSubClass</th>
      <th>MSZoning</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>Street</th>
      <th>Alley</th>
      <th>LotShape</th>
      <th>LandContour</th>
      <th>Utilities</th>
      <th>LotConfig</th>
      <th>...</th>
      <th>PoolArea</th>
      <th>PoolQC</th>
      <th>Fence</th>
      <th>MiscFeature</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SaleType</th>
      <th>SaleCondition</th>
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>60</td>
      <td>RL</td>
      <td>65.0</td>
      <td>8450</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>Inside</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>208500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>RL</td>
      <td>80.0</td>
      <td>9600</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>FR2</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>5</td>
      <td>2007</td>
      <td>WD</td>
      <td>Normal</td>
      <td>181500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>60</td>
      <td>RL</td>
      <td>68.0</td>
      <td>11250</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>Inside</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>9</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>223500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>70</td>
      <td>RL</td>
      <td>60.0</td>
      <td>9550</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>Corner</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2006</td>
      <td>WD</td>
      <td>Abnorml</td>
      <td>140000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>60</td>
      <td>RL</td>
      <td>84.0</td>
      <td>14260</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>FR2</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>250000</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 80 columns</p>
</div>



As we can see, the data are tabular. Every row represents a different house, and every column represents a different variable. In machine learning terminology, we typically refer to the rows and columns as *samples* and *features*, respectively. We can thus think of our data as a two-dimensional *n* (samples) x *p* (features) matrix. The vast majority of algorithms implemented in the scikit-learn and keras packages expect to receive numerical matrices of this kind as their primary inputs. (Note that some of the columns in our dataset—e.g., "MSZoning" and "LotShape"—contains strings or categorical values, so we need to pre-process these columns). One option would be to recode these columns into a numerical form before we could make proper use of them by defining different levels. The other option would be to just remove them. Since we have 80 features, we will just remove them for now. The original dataset consists of 80 columns and 1460 samples.
