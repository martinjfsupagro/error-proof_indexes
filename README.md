# Creating error-proof_indexes for high throughput sequencing



This document explains the rationale and method used to create error-proof indexes for high throughput sequencing. The whole repository can be cited as Jean-Francois Martin, 2019,  Creating error-proof_indexes for high throughput sequencing. Github repository https://github.com/martinjfsupagro/error-proof_indexes

[![DOI](https://zenodo.org/badge/198625228.svg)](https://zenodo.org/badge/latestdoi/198625228)





## Rationale

High throughput sequencing often involves multiplexing several samples to get cost-efficient. In such case, constructing libraries with a number of different indexes, whether included in the inserts (inline) or as external indexes read separately by the sequencers, requires that the indexes are different enough so they are not confounded. Multiple strategies exist for selecting such oligonucleotide sequences, including error-proof designs that are resistant to errors. this is particularly useful as high throughput technologies are error-prone.  The reason I designed such indexes is for amplicon analyses (metabarcoding) where we pool thousands of specimens but this could be used for any application and technology requiring multiplexing.

An clear example of combining indexes and sequencing adapters in 2-step PCR strategy is in Galan, M,  Pons, J‐B,  Tournayre, O, et al.  Metabarcoding for the parallel identification of several hundred predators and their prey: Application to bat species diet analysis. *Mol Ecol Resour*.  2018; 18: 474– 489. https://doi.org/10.1111/1755-0998.12749



## Method details

I used a R package DNAbarcodes 1.14.0 (Buschmann,  DNABarcodes: an R package for the systematic construction of DNA sample tags, *Bioinformatics*, Volume 33, Issue 6, 15 March 2017, Pages 920–922, https://doi.org/10.1093/bioinformatics/btw759)

For my particular purpose a length of 9 nucleotides was enough to provide the 384 indexes I aimed to design. The minimal distance of 3 (levseq distance model used) was chosen as it allows for autocorrecting if 1 position is erroneous. The Levseq model was chosen to account for substitutions but also potential indels as those indexes could be used in combination with PacBio or ONT technologies.

The first part of the script search for potential indexes fitting those constraints, the second part is used to subset the indexes with maximizing the distance between the required number of indexes (here 384). All of those variables are highly customizable.

See Rmd and html files for details on the script used. 

