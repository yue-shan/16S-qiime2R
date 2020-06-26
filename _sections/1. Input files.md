The following four input is required:

- A table file in .qza . This should be the table.qza from dada2 analysis or rarefied_table.qza
- A metadata file, in .tsv or .txt.
- A Taxonomy.qza file, this is generated from classifier (I use gg-13-8-99-515-806-nb-classifier.qza and rep-seq) and rep-seq.qza.It is a data.frame with Feature ID, Taxonomy and confidence.
- A rooted-tree.qza file generated from rep-seq.qza
