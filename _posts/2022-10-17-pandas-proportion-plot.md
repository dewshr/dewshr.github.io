---
title: Bar plot based on proportion for each individual group
author: Dewan Shrestha
date: 2022-10-17 15:00:00 -0500 
categories: [pandas]
tags: [pandas, seaborn, proportion, percentage, plot]
pin: false
---
Lets load the dataset

```py
import pandas as pd
import seaborn as sns

df = sns.load_dataset('tips')
df.head()

total_bill	tip	sex	smoker	day	time	size
0	16.99	1.01	Female	No	Sun	Dinner	2
1	10.34	1.66	Male	No	Sun	Dinner	3
2	21.01	3.50	Male	No	Sun	Dinner	3
3	23.68	3.31	Male	No	Sun	Dinner	2
4	24.59	3.61	Female	No	Sun	Dinner	4
```

Lets say we want to distinguish the peoples preference for lucnch or dinner based on days. We can do that combining the pandas with seaborn

```py
df['time'].groupby(df['day']).value_counts(normalize=True).rename('proportion').reset_index().set_axis(['day','time','proportion'], axis=1).pipe((sns.barplot,'data'),x='day',y='proportion',hue='time')
```
![proportion_plot](/assets/img/pandas_tricks/proportion_plot.png)
