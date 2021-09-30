---
title: ML Basics Intro
linktitle: ML Basics Intro
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ml_intro:
    parent: 04. ML Basics
    weight: 1

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

# What *is* machine learning?

Here's a working definition: **machine learning is the field of science/engineering that seeks to build systems capable of learning from experience.**

This is a very broad definition, and in practice, the set of activities that get labeled "machine learning" is pretty heterogeneous. However, two elements are common to nearly all machine learning applications: (a) the emphasis is on developing algorithms that can learn (semi-)autonomously from data, rather than static rule-based systems that must be explicitly designed or updated by humans; and (b) algorithm evaluation focuses heavily on the ability to meet objective quantitative targets.

Fundamentally, machine learning involves building mathematical models to help understand data. "Learning" enters the fray when we give these models tunable parameters that can be adapted to observed data; in this way the program can be considered to be "learning" from the data. Once these models have been fit to previously seen data, they can be used to predict and understand aspects of newly observed data.

Within the subsequent subsections we will cover the basics of machine learning including terminology and basic principles.

## Exploratory Data Analysis

In exploratory data analysis (EDA), a major component of the data science lifecycle, we summarize, visualize, and transform data in order to understand them more deeply. Through exploratory data analysis we seek to deeply understand our data. Maintaining "a state of flexibility" helps us know what to look for. Fluency with our computational tools allows us to conduct our search. In this chapter, we emphasize the necessary attitude as we introduce increasingly sophisticated tools. Although EDA varies between domains of study, we almost always begin EDA by understanding:

1. The data types of columns and the granularity of rows in the dataset.
2. The distributions of quantitative data and measures of center and spread.
3. Relationships between quantities in the dataset.
