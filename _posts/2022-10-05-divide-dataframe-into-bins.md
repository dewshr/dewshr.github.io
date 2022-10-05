---
title: Divide pandas dataframe into bins
author: Dewan Shrestha
date: 2022-08-22 13:30:00 -0500 
categories: [python, pandas]
tags: [pandas, seaborn, cut, qcut, bin]
pin: false
---
# Dividing pandas dataframe into bins using qcut and cut

Lets use a sample dataframe
```py
df = sns.load_dataset('iris')
df.head()
```
![iris_data](/assets/img/pandas_tricks/iris_data.png)

Lets say we want to divide the dataframe into **`5 bins`** based on the petal length. We can do that using `qcut or cut`.

## Using qcut
`qcut` tries to divide the dataframe into bins such that similar proportion of data numbers are present in each bin.

```py
df['qcut_bin'] = pd.qcut(df['petal_length'],5)
```

## using cut
If we use `cut` to divide into 5 bins using `petal_length`, then it will generate the bins into 5 equal proportion based on the `petal length values`.

```py
df['cut_bin'] = pd.cut(df['petal_length'],5, include_lowest=True)
```

The following picture represents different bins and numbers of data in each bin
```py
plt.figure(figsize=(15,7))
plt.subplot(1,2,1)
sns.countplot(df['qcut_bin'])
plt.xticks(rotation=90)

plt.subplot(1,2,2)
sns.countplot(df['cut_bin'])
plt.xticks(rotation=90)
```

![count_plot](/assets/img/pandas_tricks/dataframe_bin.png)