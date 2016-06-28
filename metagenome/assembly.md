---
layout: post
title:  "Metagenomics sequencing file assembly"
date:   2015-12-30 08:44:12 -0600
categories: jekyll update
---

this is the modified tutorial from http://khmer-protocols.readthedocs.org/en/v0.8.4/

## 1. Quality trimming 

~~~
for x in *R1*fastq.gz ;do echo "java -jar /usr/local/bin/trimmomatic-0.30.jar PE ${x%_R1*}_R1.fastq.gz ${x%_R1*}_R2.fastq.gz ${x%_R1*}_s1_pe ${x%_R1*}_s1_se ${x%_R1*}_s2_pe ${x%_R1*}_s2_se ILLUMINACLIP:/usr/local/share/adapters/TruSeq3-PE.fa:2:30:10 1>${x%_R1*}.log" ; done > trim-command.sh 
cat trim-command.sh | parallel
~~~


## 2. interleave-command

~~~
for x in *R1*fastq.gz ; do echo "interleave-reads.py ${x%_R1*}_s?_pe -o ${x%_R1*}interleaved.fastq" ; done > interleave-command.sh
cat interleave-command.sh | parallel
~~~

## 3. diginorm

~~~
echo "normalize-by-median.py --ksize 20 -R diginorm.report -C 20 --n_tables 4 --max-tablesize 10e9 -p -s normC20k20.kh *interleaved.fastq" > diginorm-command.sh
bash diginorm-command.sh 
~~~

## 4. error-trim

~~~
echo "filter-abund.py -V normC20k20.kh *keep" > error-trim.sh
bash error-trim.sh
~~~

## 5. extract
~~~
for x in *keep.abundfilt;do echo "extract-paired-reads.py $$x" ;done > extract.sh
cat extract.sh | parallel
~~~

## 6. final-contig
~~~
gzip *abundfilt.pe
cat *abundfilt.pe*gz > abundfilt-all.gz
~/megahit/megahit --12 abundfilt-all.gz
~~~