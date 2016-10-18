# Calculate RPKM from assembly

#### install software
```
wget http://sourceforge.net/projects/bowtie-bio/files/bowtie2/2.2.5/bowtie2-2.2.5-linux-x86_64.zip
unzip bowtie2-2.2.5-linux-x86_64.zip
mv bowtie2-2.2.5 ~/BT2_HOME
PATH=$PATH:~/BT2_HOME
export PATH
```

###After you have assembly, you want to map your raw-read onto the assembled contig to count. First, mapping (Let me say your assembly file is assembly.fna)

```
bowtie2-build assembly.fna assemblyREF
for x in ./*R1*.gz;do echo "bowtie2 -x assemblyREF -1 $x -2 ${x%R1*}R2.fastq.gz -S ${x%R1*}.sam 2> ${x$R1*}.out";done > command.bowtie2.sh
cat bowtie2.sh | parallel
```
###Use samtools to covert to bam, sort
```
for x in *.sam;do echo "samtools view -Sb $x > $x.bam";done > command.view.sh
cat command.view.sh|parallel
for x in *.bam;do echo "samtools sort $x $x.sorted";done >command.sort.sh
cat command.sort.sh|parallel
for x in *.sorted.bam;do echo "samtools index $x";done > command.index.sh
cat command.index.sh |parallel
for x in *.sorted.bam;do echo "samtools idxstats $x > $x.idxstats.txt";done > command.idxstats.sh
cat command.idxstats.sh |parallel
```
### merge count
```
git clone https://github.com/metajinomics/ngs_tools
python ngs_tools/get_count_table.py *.idxstats.txt > counts.txt
```

### calculate RPKM
```
git clone https://github.com/metajinomics/get_rpkm.git
g++ get_rpkm/Get_RPKM.cpp -o get_rpkm/Get_RPKM
./get_rpkm/Get_RPKM counts.txt normal_counts.txt
```
