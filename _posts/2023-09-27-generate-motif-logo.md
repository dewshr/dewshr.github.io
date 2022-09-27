---
title: Generate Frequency count table and motif logo from given fasta sequences
author: Dewan Shrestha
date: 2022-09-27 13:20:00 -0500 
categories: [Bioinformatics]
tags: [motif, logo, biopython, pwm, fasta, seaborn]
pin: false
---
To generate a motif logo first we need to create a count table for the nucleotide bases from fasta sequences and then information matrix to plot motif logo

# Create count table from fasta sequence

```py

import logomaker
import pandas as pd
from Bio.Seq import Seq
from Bio import motifs
import matplotlib.pyplot as plt
import seaborn as sns

seq_list = []

fasta = open(input_fasta_file,'r').readlines()

for line in fasta:
    if not line.startswith('>'):
			seq_list.append(line.upper().replace('\n',''))

	print('...... getting base counts .....\n')

	instances = [Seq(x.upper()) for x in seq_list]
	m = motifs.create(instances)

	m_df = pd.DataFrame(m.counts)
    m_df = m_df.iloc[0:10,:]
    m_df.head()

# Running above for loop gives following output
    A	C	G	T
0	239	239	351	593
1	513	231	211	467
2	281	140	771	230
3	284	451	443	244
4	410	621	156	235
```

# Generate information matrix to generate motif logo

```py
t_df = logomaker.transform_matrix(m_df, from_type = 'counts', to_type='information')


sns.set(font_scale=1.5, style='white')
plt.figure(figsize=(15,15))

crp_logo=logomaker.Logo(t_df,font_name='Arial Rounded MT Bold')
crp_logo.style_spines(visible=False)
crp_logo.style_spines(spines=['left', 'bottom'], visible=True)

plt.title('motif')
plt.tight_layout()
plt.savefig('/Users/dshresth/Downloads/test.pdf')
```
![motif](/assets/img/test.png)

Please make sure you have required packages for this to work. I also have the script [here](https://github.com/dewshr/Bioinformatics-tools-and-data/tree/main/create_motif_logo).
