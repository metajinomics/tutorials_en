# calculate RPKM for each gene on your assembly
#### htseq
```
for x in *.sorted.bam;do echo "htseq-count -f bam $x your.gtf > $x.count.txt";done > command.htseq.sh
cat command.htseq.sh|parallel
```

#### get count table
```
git clone https://github.com/metajinomics/ngs_tools.git
python ngs_tools/htseq_to_count.py your.gtf *bam.count.txt > counts.txt
```

#### calculate RPKM
```
git clone https://github.com/metajinomics/get_rpkm.git
g++ get_rpkm/Get_RPKM.cpp -o get_rpkm/Get_RPKM
./get_rpkm/Get_RPKM counts.txt normal_counts.txt
```
