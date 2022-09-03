---
title: Create Genome Index file to map sequencing data
author: Dewan Shrestha
date: 2022-09-03 00:30:00 -0500 
categories: [Bioinformatics]
tags: [index, bwa, star, bowtie2, kallisto, rna sequencing, dna sequencing, alignment]
pin: false
---

There are several tools available map sequencing data to the reference genome. And for all of the tools index files needs to be generated first. Here are some of the tools and the syntax used to generate index file.


## DNA Sequence

**Burrows-Wheeler Alignment Tool ([bwa](http://bio-bwa.sourceforge.net/bwa.shtml))**

```sh
bwa index hg38.fa
```
**[Bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml)**

```sh
bowtie2-build hg38.fa index_filename
```
<br/>

## RNA Sequence

**Spliced Transcripts Alignment to a Reference ([STAR](https://physiology.med.cornell.edu/faculty/skrabanek/lab/angsd/lecture_notes/STARmanual.pdf))**

```sh
STAR --runThreadN 20 --runMode genomeGenerate --genomeDir index_files/star_2.5.3a --genomeFastaFiles hg38.fa --sjdbGTFfile gencode.v41.annotation.gtf --sjdbOverhang 99
```
`sjdbOverhang value = readlength - 1`

**[kallisto](https://pachterlab.github.io/kallisto/manual)**

kallisto doesn't allign sequencing reads to the genome, it performs pseudoalignment for transcript quantification using indexed transciptome. You can download the `cdna fasta` sequence from [ensembl site](https://useast.ensembl.org/info/data/ftp/index.html).

![pseudo_alignment](/assets/img/pseudoalignment.png)
```sh
kallisto index -i index_filename hg38.cdna.fa
```

`example: index_filename = hg38_index.idx`

<br/>

## Reference

-   https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4631051/
-   https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3322381/