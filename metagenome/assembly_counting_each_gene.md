# calculate RPKM for each gene on your assembly

#### install bowtie2
```
wget http://sourceforge.net/projects/bowtie-bio/files/bowtie2/2.2.5/bowtie2-2.2.5-linux-x86_64.zip
unzip bowtie2-2.2.5-linux-x86_64.zip
mv bowtie2-2.2.5 ~/BT2_HOME
PATH=$PATH:~/BT2_HOME
export PATH
```

#### run bowtie2
```
bowtie2-build assembly.fna assemblyREF
for x in ./*R1*.gz;do echo "bowtie2 -x assemblyREF -1 $x -2 ${x%R1*}R2.fastq.gz -S ${x%R1*}.sam 2> ${x$R1*}.out";done > command.bowtie2.sh
cat bowtie2.sh | parallel
for x in *.sam;do echo "samtools view -Sb $x > $x.bam";done > command.view.sh
cat command.view.sh|parallel
for x in *.bam;do echo "samtools sort $x $x.sorted";done >command.sort.sh
cat command.sort.sh|parallel
for x in *.sorted.bam;do echo "samtools index $x";done > command.index.sh
cat command.index.sh |parallel
```
#### find orf
```
wget http://downloads.sourceforge.net/project/fraggenescan/FragGeneScan1.30.tar.gz
tar -zxvf FragGeneScan1.30.tar.gz
cd FragGeneScan1.30/
make fgs
cd ..
./FragGeneScan1.30/run_FragGeneScan.pl -genome=metaT.assembly.fa -out=orf -complete=0 -train=illumina_5
```

#### run htseq
```
git clone https://github.com/metajinomics/ngs_tools.git
python ngs_tools/fix_gtf.py your.gff > your.gtf
for x in *.sorted.bam;do echo "htseq-count -f bam $x your.gtf > $x.count.txt";done > command.htseq.sh
cat command.htseq.sh|parallel
```

#### get count table
```
python ngs_tools/htseq_to_count.py your.gtf *bam.count.txt > counts.txt
```

#### calculate RPKM
```
git clone https://github.com/metajinomics/get_rpkm.git
g++ get_rpkm/Get_RPKM.cpp -o get_rpkm/Get_RPKM
./get_rpkm/Get_RPKM counts.txt normal_counts.txt
```
