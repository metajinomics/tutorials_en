---
layout: post
title:  "Assembly Evaluation"
date:   2016-05-06 16:04:12 -0600
categories: jekyll update
---

## Assembly and Assembly evaluation 
The goal of this tutorial is to show you how to assembly and evaluate

### Amazon AMI
First, install nessesary program

### Packages to install
khmer
```
pip install khmer
```
PSAdes

Quast

### Getting the data
Let's create a working directory
```
cd /mnt
mkdir assembly
cd assembly
```
Download E. coli data
```
curl -O https://s3.amazonaws.com/public.ged.msu.edu/ecoli_ref-5m-trim.fastq.gz
```

### Running an assembly
Run spades

### Looking at the assembly
Run Quast

### Comparing and evaluating assemblies
Quast

### other assembly - MEGAHIT

### reference free comparison