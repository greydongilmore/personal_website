---
title: Data Transformations
linktitle: Data Transformations
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ml_intro:
    parent: 03. Data Pre-processing
    weight: 4

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 4
---

Transformations of predictor variables may be needed for several reasons. Some modeling techniques may have strict requirements, such as the predictors having a common scale. In other cases, creating a good model may be difficult due to specific characteristics of the data (e.g., outliers). There are several methods to transform data prior to modelling, which include: standardization, min-max scaling and unit vector normalization.

## Standardization (Z normalization)

The most straightforward and common data transformation is to standardize the data. To standardize the data, the average predictor value is subtracted from all the values. As a result of standardizing, the predictor has a mean of 0 and a standard deviation of 1.

We will use scikit-learn function **StandardScaler**:

```python
# Standardize data (0 mean, 1 stdev)
from sklearn.preprocessing import StandardScaler
import pandas
import numpy
from sklearn import datasets

# Load a dictionary (technically, a Bunch) containing the data
iris = datasets.load_iris()

# 'data' and 'target' contains the feature data and classes, respectively
X, y = iris['data'], iris['target']

scaler = StandardScaler().fit(X)
rescaledX = scaler.transform(X)

# summarize transformed data
print(rescaledX[0:5,:])
```

    [[-0.90068117  1.01900435 -1.34022653 -1.3154443 ]
     [-1.14301691 -0.13197948 -1.34022653 -1.3154443 ]
     [-1.38535265  0.32841405 -1.39706395 -1.3154443 ]
     [-1.50652052  0.09821729 -1.2833891  -1.3154443 ]
     [-1.02184904  1.24920112 -1.34022653 -1.3154443 ]]
    

The values for each attribute now have a mean value of 0 and a standard deviation of 1.

## Min-Max Normalization (Rescale)

When your data is comprised of attributes with varying scales, many machine learning algorithms can benefit from rescaling the attributes to all have the same scale. Often this is referred to as min-max normalization and attributes are often rescaled into the range between 0 and 1. This is useful for optimization algorithms used in the core of machine learning algorithms like gradient descent. It is also useful for algorithms that weight inputs like regression and neural networks and algorithms that use distance measures like K-Nearest Neighbors.

We will use scikit-learn function **MinMaxScaler**:


```python
# Rescale data (between 0 and 1)
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler(feature_range=(0, 1))
rescaledX = scaler.fit_transform(X)

# summarize transformed data
print(rescaledX[0:5,:])
```

    [[0.22222222 0.625      0.06779661 0.04166667]
     [0.16666667 0.41666667 0.06779661 0.04166667]
     [0.11111111 0.5        0.05084746 0.04166667]
     [0.08333333 0.45833333 0.08474576 0.04166667]
     [0.19444444 0.66666667 0.06779661 0.04166667]]
    

The rows are normalized to length 1.

## Unit Vector Normalization

Each sample (i.e. each row of the data matrix) with at least one non zero component is rescaled independently of other data samples so that its norm equals 1 (called a unit norm in linear algebra). This preprocessing can be useful for sparse datasets (lots of zeros) with attributes of varying scales when using algorithms that weight input values such as neural networks and algorithms that use distance measures such as K-Nearest Neighbors.

We will use scikit-learn function **Normalizer**:


```python
# Normalize data (length of 1)
from sklearn.preprocessing import Normalizer

scaler = Normalizer().fit(X)
normalizedX = scaler.transform(X)

# summarize transformed data
print(normalizedX[0:5,:])
```

    [[0.80377277 0.55160877 0.22064351 0.0315205 ]
     [0.82813287 0.50702013 0.23660939 0.03380134]
     [0.80533308 0.54831188 0.2227517  0.03426949]
     [0.80003025 0.53915082 0.26087943 0.03478392]
     [0.790965   0.5694948  0.2214702  0.0316386 ]]
    

The rows are normalized to length 1.
