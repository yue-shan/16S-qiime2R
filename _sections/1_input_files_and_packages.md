## The following four input is required:

- A table file in .qza . This should be the table.qza from dada2 analysis or rarefied_table.qza
- A metadata file, in .tsv or .txt.
- A Taxonomy.qza file, this is generated from classifier (I use gg-13-8-99-515-806-nb-classifier.qza and rep-seq) and rep-seq.qza.It is a data.frame with Feature ID, Taxonomy and confidence.
- A rooted-tree.qza file generated from rep-seq.qza

## R Package required
```
library(devtools) #only need this one to install others
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
## Load all files into a Phyloseq object
In this step, we will use the input data to create a Phyloseq object. For more info on phyloseq, refer to [https://joey711.github.io/phyloseq/](https://joey711.github.io/phyloseq/)

- first, read the files into R. Here I started with .qza file. We can also import these data from txt or excel files. 
```
library(qiime2r)
library(phyloseq)
metadata<-read_q2metadata("metadata.txt")
  head(metadata)

OTUs<-read_qza("rarefied_table.qza")
  OTUs$data[1:10,1:10] #show first 10 taxa within first 15 samples

taxonomy<-read_qza("taxonomy_gg.qza")
head(taxonomy$data)
```

- Create a Phyloseq Object named phylo, which contains sample ID and metadata info, abundance of each OTU in each sample, and their taxonomy information.

```
phylo<-qza_to_phyloseq(
  features="rarefied_table.qza",
  tree="rooted-tree.qza",
  "taxonomy_gg.qza",
  metadata = "metadata.txt")
phylo
```

- let's check if phylo is created correctly
```
rank_names(phylo) 
sample_variables(phylo)
sample_names(phylo)
get_taxa_unique(phylo, "Family")[1:10]
tax_table(phylo)[1:10] 
sample_data(phylo)
levels(sample_data(phylo)$TreatmentWeek)
levels(sample_data(phylo)$Genotype)
```
If any of the above is "NULL", something is not right and you need to check the original file. 
The levels are ordered alphabetically. You can reorganize the order of the levels by define a new vector for them. For example, new -> c(sample_data(phylo)$TreatmentWeek, levels = c("a","b")).

