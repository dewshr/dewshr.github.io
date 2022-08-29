---
title: Pandas Tricks
author: Dewan Shrestha
date: 2022-08-24 16:45:00 -0500 
categories: [python, pandas]
tags: [pandas, filter, fimo, tricks, transription_factors]
---

## Splitting a row into multiple rows based on substring in a specific column

Here I have a dataframe with 3 columns `(p1, p2 and tissue)`. In column `p2` I have 2 genes separated by **`';'`**

```ruby
import pandas as pd

pp = pd.read_csv('promoter_promoter.csv', skiprows=2, names=['p1','p2','tissue'])

pp.head()
```
![pandas_tricks1](/assets/img/pandas_tricks/pandas_tricks1.png)

You can split each of those rows into separate rows by:
```ruby
pp = pp.assign(p2=pp["p2"].str.split(";")).explode("p2")

pp.head(n=7)
```
![pandas_tricks2](/assets/img/pandas_tricks/pandas_tricks2.png)


<br/>

## Filter out the rows only selecting minimum value based on a specific column

I mainly use this to filter out the output file from program [fimo](https://meme-suite.org/meme/tools/fimo). While scanning for motifs in a given sequnce, there can be multiple region within the sequence where a motif can be found. And I only want to keep those regions with the most significant motifs if there are multiple motifs identified in a given sequence.
Here, in this dataframe, `chr10:103057760-103058020` and `chrX:23926122-23926382` has motifs in two positions and  `chr10:103362455-103362715` in three.

```ruby
import pandas as pd

fimo_df = pd.read_csv('fimo.tsv',sep='\t').iloc[0:-3,:]

fimo_df.head()
```  

![fimp_filter1](/assets/img/pandas_tricks/fimo_filter1.png)

I am using `iloc` to remove last 3 rows from the fimo output file, which contains program run information. Now, since there are mulitple values for same `sequence_name`, I will only be keeping the one with lowest `p-value`

```ruby
fimo_df = fimo_df.loc[fimo_df.groupby('sequence_name')['p-value'].idxmin()]

fimo_df.head()
```

![fimp_filter2](/assets/img/pandas_tricks/fimo_filter2.png)

<br/>


## Filtering dataframe if substring in a column matches to any elements of a list

Lets assume we have a dataframe as below:

`df.head()`
![pandas_tricks3](/assets/img/pandas_tricks/pandas_tricks3.png)

And we want to filter out the dataframe based on our list of transcription factors (TF) as:
`tf_list = ['BATF','PBX3']`

Since, the TF we are interested is a substring in column `motif_id`, we can't use `df[df['motif_id']].isin(tf_list)`. So, we can achieve that by:

![pandas_tricks4](/assets/img/pandas_tricks/pandas_tricks4.png)

In the code, above we are also using `.upper()` function to convert all letters to uppercase if there are any lowercase letters.

