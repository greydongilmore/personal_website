---
title: Input Variables
linktitle: Input Variables
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ml_intro:
    parent: 03. Data Pre-processing
    weight: 3

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3
---

Having some features we can use to make predictions is great, but we also need to know what we're trying to predict! Conventionally, the target of the prediction process is a vector of scores usually labeled **y**. The features are thus seperated into two main variables denoted with **X** and **y**. The **X** variable will contain all of the features and samples except for the output or target feature sale price. We are using sale price as our target predictor feature, which gets assigned to the **y** variable.


```python
from sklearn.model_selection import train_test_split

# Set final input features and output variable
y = X['SalePrice']
X = X.drop(['SalePrice'], axis =1)

# Split data into test and train sets
X_train, X_test, y_train, y_test = train_test_split(X, y.to_numpy().ravel(), test_size=0.30, random_state=101)
```

The first approach to remove some of the features will be to examine the correlation between the features and the independent variable (target) of sale price:


```python
import seaborn as sns

# matplotlib is Python's main plotting library.
# the plt module provides high-level access to plots.
import matplotlib.pyplot as plt

### tells the jupyter notebook to display plots in-line
%matplotlib inline

# Select only columns that are numeric
all_data = all_data.select_dtypes(['number'])

# Create correlation matrix
correlation_matrix = all_data.corr()

fig, ax = plt.subplots(figsize=(10,7)) 
sns.heatmap(data=correlation_matrix, annot=True, ax=ax);
```

We will now remove features that have a low correlation with sales price as these features to not contribute significantly:


```python
# Correlation with output variable
cor_target = abs(correlation_matrix["SalePrice"])

# Selecting correlated features above threshold
relevant_features = cor_target[cor_target>0.1]
X = all_data[relevant_features.index.values]

# Remove any rows that contain NaN
for ifeature in relevant_features.index.values:
    X = X[pd.notnull(X[ifeature])]
```


```python
# Histogram of the sales
X['SalePrice'].plot(kind='hist', color='purple', edgecolor='black', figsize=(10,6), bins = 30);
plt.title('Distribution of House Sale Price', fontweight='bold');
plt.xlabel('Sale Price (USD)', fontweight='bold');
plt.ylabel('Frequency', fontweight='bold');
```

The cleaned-up version of the distribution of sales price, the dataset now contains 1121 samples and 27 features.
