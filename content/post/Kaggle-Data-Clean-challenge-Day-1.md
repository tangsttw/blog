---
title: "Kaggle Data Clean Challenge Day 1 - Missing Values"
date: 2018-04-08T14:17:37+08:00
draft: false
description: ""
tags: [Kaggle, Data Science]
categories: [Kaggle]
author: "YT"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: false
autoCollapseToc: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
mathjax: true
---

Kaggle DCC Day 1 Handling Missing values
===
This is the note for day 1 of the 5-day data challenge held by Kaggle. In the first day, the topic is how to deal with missing values.

[Notebook code of the challenge](https://www.kaggle.com/tangsttw/data-cleaning-challenge-handling-missing-values)

## Intro
Data science is a science based on data and is highly related to data; the quality of data has huge effect on the result. Therefore, it is important to ensure the data quality before executing any analysis on data.
Generally, raw data contains some dirty data, and data cleaning is what we need to do right after we recieve a new dataset. The higher quality we have, the better prediction or analysis we can make from the data.

At the first step of data cleaning, we deal with missing values. Sometimes, due to various reasons, there may be several misssing values in data. We need to find them out and fix them.
Basically, handling missing values can be separate into five part described as following :

- [First look at the data](#First-look-at-the-data)
- [How many missing data are there](#How-many-missing-data)
- [Figure out the reason why data is missing](#Figure-out-why-data-is-missing)
- [Drop missing values](#Drop-missing-values)
- [Fill in missing values](#Fill-in-missing-values)


## First look at the data
The first thing to do with a new dataset is take a look at some of it. This gives a glimpse of the data and helps get an idea of what's going on with the data. We sample several records from the data to perform this step.
Through this step, you can have some knowledge of how data look like and if there is something strange in data.

In python, we usually use `pandas` to load data and perform data manipulations. For this step,
> use pandas's sample(n) function


## How many missing data
If we noticed that there are some missing values in data, we would like to known how many missing data are there is data and the distribution of missing data. In this step, normally we calculate the number of missing values in each feature column, sum up the total, and then calculate the portion of the missing data in the dataset.
In python pandas, we are looking for `NaN` vaules which represents missing values. Pandas provides a `isnull()` function to detect whether the data is a `NaN`.


## Figure out why data is missing
There are basically two conditions that data is missing
- The data doesn't exist
- The data is not recorded

Read the data description in the documentation of the dataset to check how the data is collected (automatic fillin or user input) and the meaning of the data; then, use the information to figure out in which condition the missing data is. After understanding the reason, there will be basically two different ways to deal with the missing value respectively.
- [Drop the data](#Drop-missing-values) for the data doesn't exist.
- [Fill in values](#Fill-in-missing-values) for the data is not recorded.

For more advanced techniques about dealing missing values, search with the following kewords.
Keywords for further reference : `data intution`, `imputation`

## Drop missing values
If the value is missing because it doesn't exist (e.g. there won't be any record about child's age if the person doesn't have child), we should consider to drop them or intentionally keep them as Nan (or set another value representing no-exist).

## Fill in missing values
The alternative way to deal with missing values is guess a value and fill them in.
There are several methods to guess the value. Some of them are really simple and fast but naive, some fo them are more complicated and accurate but requires some technique. Which one is better depends on the data. The followings are the ways that you can fill the data cell wit,
* average of the column of data
* regression to predict the data
* missing observation correlation
* maximum likelihood method

With the guessed value in substitution of missing values, you can use `fillna()` function in python pandas.


## Summary
It seems easy in handling missing values, but actually, it plays an important role in the performance of your analysis and prection result; The qulity of data to some extent influences the performance of algorithms. It requires more effort on data cleaning process.
There are more knowledge about data intution, imputation, and methods to fill in missing values for further survey.
