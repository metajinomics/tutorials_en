# Calculate RPKM from assembly
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
git clone https://github.com/edamame-course/Metagenome.git
python Metagenome/get_count_table.py *.idxstats.txt > counts.txt
```

### calculate RPKM
```
git clone https://github.com/metajinomics/get_rpkm.git
g++ get_rpkm/Get_RPKM_for_assembly.cpp -o get_rpkmGet_RPKM_for_assembly 
./get_rpkm/Get_RPKM_for_assembly counts.txt normal_counts.txt
```
