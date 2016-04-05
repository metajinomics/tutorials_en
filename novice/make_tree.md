---
layout: post
title:  "How to make a tree"
date:   2016-02-12 13:59:12 -0600
categories: jekyll update
---

## How to make a tree
This tutorial shows how to make a tree such as this
![tree](https://raw.githubusercontent.com/metajinomics/tutorials_en/gh-pages/novice/files/new_tree_gc_new_name_box.png)
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
```
cat your_16s.fa type_strain.fa > all_seq.fa
```
### Alignment for generate tree
Infernal
```
cmalign bacteria_model.cm QueryBacteria.txt > bac_ali.sto
esl-reformat afa bac_ali.sto > bac_ali.afa
```
### Generate tree
Fasttree
```
./FastTree -nt <  new_tree_edited_name.afa > afa.tree
```


