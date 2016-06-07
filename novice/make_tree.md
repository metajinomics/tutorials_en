---
layout: post
title:  "How to make a tree"
date:   2016-02-12 13:59:12 -0600

---

## How to make a tree
This tutorial shows how to make a tree such as this
![tree](https://raw.githubusercontent.com/metajinomics/tutorials_en/gh-pages/novice/files/new_tree_gc_new_name_box.png)
Lian, J., Choi, J., Tan, Y. S., Howe, A., Wen, Z., & Jarboe, L. R. (2016). Identification of Soil Microbes Capable of Utilizing Cellobiosan. PLoS ONE, 11(2), e0149336. http://doi.org/10.1371/journal.pone.0149336
### Download seq for type strain
[Download sequences](https://raw.githubusercontent.com/metajinomics/tutorials_en/gh-pages/novice/files/list_type_strain.txt)
This file contains Ids
### fetch 16s seq from type strain
```
python fetch_genome.py id.txt foldername
cd foldername
cat *.fa type_strain.fa
```
### add your baby seq
You may have 16s rRNA sequence that you isolated. You can use 16s rRNA primer for PCR then sequence it. [Here](https://en.wikipedia.org/wiki/16S_ribosomal_RNA) is some univertial primers.
```
cat your_16s.fa type_strain.fa > all_seq.fa
```
### Alignment for generate tree
[Infernal](http://eddylab.org/infernal/) aligns 16s rRNA sequences. This program requires model file. We use 16s bacterial model built by RDP. 16s rRNA is well studied compared to other sequences. So, we can take a benefit to use model to align the sequences. 
```
cmalign bacteria_model.cm all_seq.fa > bac_ali.sto
esl-reformat afa bac_ali.sto > bac_ali.afa
```
### Generate tree
[Fasttree](http://www.microbesonline.org/fasttree/) builds maximum-likelihood phylogenetic trees. It uses Jukes-Cantor(default) or generalized time-reversible (GTR) models of nucleotide.
```
./FastTree -nt <  bac_ali.afa > afa.tree
```
### Visualization
```
tree <- read.tree(file="~/Documents/Research/2016/1january/Lian/new_tree_gc_new_name.tree")
library(phytools)
plotTree(tree,fsize=0.5,ftype="i")
```


