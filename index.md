---
layout: page
title: 16S-qiime2R
name: index
---

Welcome to 16S-qiime2R. We will use R to analyze 16S sequencing data from qiime2 pipeline. 

## Document needed
The following four input is required:

- A table file in .qza . This should be the table.qza from dada2 analysis or rarefied_table.qza
- A metadata file, in .tsv or .txt.
- A Taxonomy.qza file, this is generated from classifier (I use gg-13-8-99-515-806-nb-classifier.qza and rep-seq) and rep-seq.qza.It is a data.frame with Feature ID, Taxonomy and confidence.
- A rooted-tree.qza file generated from rep-seq.qza

## Library needed
```
library(devtools) 
library(phyloseq) 
library(qiime2R) 
library(readr) 
library(ape) 
library(ggplot2) 
library(Biostrings) 
library(biomformat) 
library(Hmisc) 
library(yaml) 
library(tidyr) 
library(plyr) 
library(dplyr) 
library(stats) 
library(utils) 
library(sqldf) 
library(vegan) 
library(stringr)
```
[sections](/_sections)

[input files](https://github.com/yue-shan/16S-qiime2R/blob/master/_sections/1_input_files.md)

