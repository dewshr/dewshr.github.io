---
title: Creating Multiple Subplots in One Figure Using Seaborn Python
author: Dewan Shrestha
date: 2022-08-22 13:30:00 -0500 
categories: [python, pandas]
tags: [seaborn, matplotlib, subplots, rcparam]
---

If you want to include multiple plots in a single figure, you can do that by creating axes. Here, is the sample code for that.

In this section of code I am just loading the example dataset.

```ruby
import searborn as sns
import matplotlib
import matplotlib.pyplot as plt
matplotlib.rcParams['pdf.fonttype'] = 42
matplotlib.rcParams['ps.fonttype'] = 42


data = sns.load_dataset('tips')
tips.head()

total_bill	tip	sex	smoker	day	time	size
0	16.99	1.01	Female	No	Sun	Dinner	2
1	10.34	1.66	Male	No	Sun	Dinner	3
2	21.01	3.50	Male	No	Sun	Dinner	3
3	23.68	3.31	Male	No	Sun	Dinner	2
4	24.59	3.61	Female	No	Sun	Dinner	4

```


After loading the data you can use following code for subplots

```ruby
cols = ['sex','smoker','day', 'time']

fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(10,10))
fig.subplots_adjust(wspace=0.5, hspace=0.5)

for ax, x in zip(axes.flatten(), cols):
    sns.boxplot(x=x, ax=ax, y='total_bill', data =tips)
    ax.set_title(f'comparison of total bills among different {x}', pad=15)

plt.savefig('/your/path/plot.pdf')
```
In the above code, wspace and hspace adjusts the space between plots and pad set the space between the subplot title and plot. You should be getting the image shown below.

![subplots](/assets/img/subplots.png)

You can also use:
```
plt.subplot(num_row, num_column, figure1)
sns.boxplot()

plt.subplot(num_row, num_column, figure2)
sns.boxplot()

plt.subplot(num_row, num_column, figure3)
sns.boxplot()

plt.subplot(num_row, num_column, figure4)
sns.boxplot()
```


