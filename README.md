# BSIAB_CC92-ST208_in_China
 This repository contains the analysis scripts that were written and used in the article of "**National genomic epidemiology and phylodynamics of Acinetobacter baumannii bloodstream isolates in China: the population superseding and toxification within CC92**".
 
 The links below the sub-headings lead to the scripts needed for the corresponding steps. Most of the scripts were developed for running on the Ubuntu 18.04.6 LTS server. You may download and adapt the scripts to suit your own requirements.

## 1. Database and software used in this workflow
### Database
- [COG](https://www.ncbi.nlm.nih.gov/research/cog/)
- [CARD](https://card.mcmaster.ca/)
- [VFDB](http://www.mgc.ac.cn/VFs/)
- [BacMet](http://bacmet.biomedicine.gu.se/)
- [pubMLST](https://pubmlst.org/)
- [isfinder](https://isfinder.biotoul.fr/about.php)
- [ICEberg](https://tool2-mml.sjtu.edu.cn/ICEberg3/index.html)
- [PHASTER](http://phaster.ca/)
- [Islandviewer4](https://www.pathogenomics.sfu.ca/islandviewer)

### Software
- [R](https://www.r-project.org/)
- [Perl](https://www.perl.org/)
- [Python3](https://www.python.org/)
- [PRINSEQ-lite](https://github.com/uwb-linux/prinseq)
- [SPAdes](https://github.com/ablab/spades)
- [QUAST](https://github.com/ablab/quast)
- [FastANI](https://github.com/ParBLiSS/FastANI)
- [Prokka](https://github.com/tseemann/prokka)
- [mlst](https://github.com/tseemann/mlst)
- [Kaptive](https://github.com/klebgenomics/Kaptive)
- [Phytools](https://cran.r-project.org/web/packages/phytools/index.html)
- [RAxML](https://evomics.org/learning/phylogenetics/raxml/)
- [Gubbins](https://github.com/nickjcroucher/gubbins)
- [BEAST2](https://www.beast2.org/)



## 2. Reads trimming
### PRINSEQ-lite
`prinseq-lite -verbose -fastq filename_clean_1.fq -ns_max_p 10 -min_qual_mean 25 -out_good filename_1_good -out_bad filename_1_bad
prinseq-lite -verbose -fastq filename_clean_2.fq -ns_max_p 10 -min_qual_mean 25 -out_good filename_2_good -out_bad filename_2_bad`

## 3. Assembly
### SPAdes
`spades.py -1 filename_1_good.fastq -2 filename_2_good.fastq --phred-offset 33 -o filename -t 30 -m 1024`

## 4. Genome assembly evaluation
### QUAST
`quast -t 10 -o filename_N50 filename.fasta`

## 5. Amino acid identity (ANI) calculation
### FastANI
`fastANI --ql list.txt --rl list.txt --matrix -t 40  -o ani.txt`

## 6. Genome annotation
### Prokka
`prokka --compliant --kingdom Bacteria \
	--genus Acinetobacter \
	--species baumannii \
	--cpus 20 \
	--outdir outdirname \
	--prefix filename \
	filename.fasta`

## 7. ST identification and diversity analysis
### mlst
`mlst --scheme abaumannii --minid 100 --mincov 100 --threads 40 filename.fasta >> oxford_mlst.txt`

### diversity analysis
Diversity indices of ST s were calculated via a custom script available on GitHub (https://github.com/ahmedmagds/rarefaction-curves).

## 8. Identification of surface polysaccharide synthesis sites
### Kaptive
A step-by-step tutorial is available [here](https://bit.ly/kaptive-workshop).








