#mapping and counting
This tutorial shows mapping and counting that using metagenome with multiple samples

if you are interested in an example of mapping for SNP, visit [here](https://github.com/edamame-course/2016-tutorials/blob/master/Metagenome/2016-07-15-mapping-counting.md)

## data downloada
assembly file will be a reference
multiple sequence files


## mapping
bwa

## counting Make count table
samtolls
```
samtools mpileup -f REL606.fa SRR098038.sorted.bam > SRR098038.mpileup
```
use gff to count

```
pip install HTSeq
```
data
```
wget ftp://ftp.ensemblgenomes.org/pub/release-29/bacteria//gtf/bacteria_5_colle\
ction/escherichia_coli_b_str_rel606/Escherichia_coli_b_str_rel606.GCA_000017985\
.1.29.gtf.gz
gunzip Escherichia_coli_b_str_rel606.GCA_000017985.1.29.gtf.gz
samtools view -h -o SRR098038.sorted.sam SRR098038.sorted.bam
htseq-count SRR098038.sam Escherichia_coli_b_str_rel606.GCA_000017985.1.29.gtf
```

## make one file
