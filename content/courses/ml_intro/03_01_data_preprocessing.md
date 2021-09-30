---
title: Data Processing Intro
linktitle: Data Processing Intro
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ml_intro:
    parent: 03. Data Pre-processing
    weight: 1

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

Data pre-processing techniques generally refer to the addition, deletion, or transformation of training set data. Different models have different sensitivities to the type of predictors in the model; *how* the predictors enter the model is also important. Transformations of the data to reduce the impact of data skewness or outliers can lead to significant improvements in performance. 

In general, the work required to make your dataset easy to analyze.

* Easy to use column names
* Fixing inconsistent variables
* Merging with other datasets
* Reshaping (melt, pivot, ect..)
* Dealing with missing values
