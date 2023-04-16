In this example, we try to assemble and annotate Escherichia coli genome using Illumina data, Oxford Nanopore data and a combination of both
## Downloading Raw Data
### fastq-dl was used to download raw genomic data from SRA or ENA

**INSTALLATION**

Conda

conda create --name fastq-dl-env -c conda-forge -c bioconda fastq-dl

for help:

https://github.com/rpetit3/fastq-dl

**USAGE**

First, activate conda env created before:

conda activate fastq-dl-env 

Illumina raw data was obtained from SRA id SRR17760777 using command bellow:

fastq-dl -a SRR17760777

Oxford Nanopore raw data was obtained from SRA id SRR10032546 using command bellow:

fastq-dl -a SRR10032546

**UNTAR ARCHIVES**

It's not mandatory to do this step because fastqc and trimmomatic can run with .gz files

gunzip SRR17760777_* 

gunzip SRR10032546.fastq.gz 

## Quality Control
### fastqc was used to check Illumina raw genomic data quality
#### This step can be done before and after trimmage, to check how was the process
**INSTALLATION**

Conda

conda create --name fastqc-env -c conda-forge -c bioconda fastqc

**USAGE**

Activating fastqc environment:

conda activate fastqc-env

fastqc ../SRR17760777_*

### Nanoplot was used to check Nanopore raw genomic data quality
#### This step can be done before and after trimmage, to check how was the process
**INSTALLATION**

Conda

conda create --name nanoplot-env -c conda-forge -c bioconda nanoplot

**USAGE**

Activating NanoPlot environment:

conda activate nanoplot-env

NanoPlot --fastq SRR10032546_1.fastq

## Trimmomatic was used to remove bad reads and adapters from Illumina data

**INSTALLATION**

Conda

conda create --name trimmomatic-env -c conda-forge -c bioconda trimmomatic

**USAGE**

Activating Trimmomatic environment:

conda activate trimmomatic-env

wget https://raw.githubusercontent.com/timflutre/trimmomatic/master/adapters/TruSeq3-PE-2.fa

trimmomatic PE -phred33 SRR17760777_1.fastq SRR17760777_2.fastq SRR17760777_1_paired.fastq SRR17760777_1_unpaired.fastq SRR17760777_2_paired.fastq SRR17760777_2_unpaired.fastq ILLUMINACLIP:TruSeq3-PE-2.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36

## NanoFilt was used to remove bad reads and adapters from Nanopore data

**INSTALLATION**

Conda

conda create --name nanofilt-env -c conda-forge -c bioconda NanoFilt

**USAGE**

Activating NanoFilt environment:

conda activate nanofilt-env

NanoFilt -q 5 --headcrop 40 SRR10032546_1.fastq

## spades was used to assemble genome only with illumina NGS data

**INSTALLATION**

Conda

conda create --name spades-env -c conda-forge -c bioconda spades

**USAGE**

Activating Spades environment:

conda activate spades-env

spades.py --pe1-1 SRR17760777_1_paired.fastq --pe1-2 SRR17760777_2_paired.fastq --pe1-s SRR17760777_1_unpaired.fastq --pe1-s SRR17760777_2_unpaired.fastq -o ../assembly

## Flye was used to assemble genome with only Nanopore data

**INSTALLATION**

Conda

conda create --name flye-env -c conda-forge -c bioconda Flye

**USAGE**

Activating Flye environment:

conda activate flye-env

flye --nano-hq -o ../assemblySRR10032546_1.fastq -o ./

## UNicycler was used to assemble genome with Nanopore and Illumina data

**INSTALLATION**

Conda

conda create --name unicycler-env -c conda-forge -c bioconda unicycler

**USAGE**

Activating Unicycler environment:

conda activate unicycler-env

unicycler -1 ../illumina_data/SRR17760777_1.fastq -2 ../illumina_data/SRR17760777_2.fastq -l ../nanopore_data/SRR10032546_1.fastq -o ./

## BUSCO and QUAST were used to evaluate genomes assemblies

**INSTALLATION**

Conda

conda create --name busco-env -c conda-forge -c bioconda busco

conda create --name quast-env -c conda-forge -c bioconda quast

**USAGE**
 
 conda activate quast-env
 
 quast.py contigs.fasta -r ../../reference_genome/ncbi-genomes-2023-04-08/GCF_000005845.2_ASM584v2_genomic.fna -1 ../SRR17760777_1.fastq -2 ../SRR17760777_2.fastq -o ../assembly_ev/quast/

# Results

## Assembly

# Annotation
