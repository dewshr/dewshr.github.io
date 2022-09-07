---
title: Calculating phyloP conservation score over certain genomic region
author: Dewan Shrestha
date: 2022-09-07 12:30:00 -0500 
categories: [Bioinformatics]
tags: [phylop, conservation, evolution, bedtools]
pin: false
---
[phyloP scores](https://genome.cshlp.org/content/20/1/110) can be used to identify the evolionary rate of genomic sequences. **Positive score** represents slower evolution or more conserved sequence and **negative score** represents faster evolution.

Pre-calculated phylop scores can be downloaded from [UCSC site]({% post_url 2022-08-31-public-data-links%}). The file is in `bigwig` format. Here, is step by step to calculate the phylop score for the given genomic region

<br/>

-   **convert `bigwig` to `bedGraph file`**

```sh
bigWigToBedGraph hg19.100way.phyloP100way.bw hg19.100way.phyloP100way.bedGraph
```

`bigWigToBedGraph` can be downloaded from [here](http://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64.v385/)

<br/>

-   **Use [bedtools map](https://bedtools.readthedocs.io/en/latest/content/tools/map.html) to get mean score over the given genomic coordinates**

```sh
bedtools map -a genomic_region.bed -b hg19.100way.phyloP100way.bedGraph -c 4 -o mean > phylop_score.bed
```
The parameter `-c 4` means the phylop score is present in column 4 in the `bedGraph` file. You can also change the output to be based on other operators such as `sum, count, median` etc.

**References**
- [paper](https://genome.cshlp.org/content/20/1/110)
-   [tutorial](http://compgen.cshl.edu/phast/phyloP-tutorial.php)
-   [phylop](https://ionreporter.thermofisher.com/ionreporter/help/GUID-03D1F68A-E646-4B49-AD59-AF2F51874BD2.html#:~:text=phyloP%20scores%20measure%20evolutionary%20conservation,are%20predicted%20to%20be%20conserved)