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

fastq-dl SRR17760777

Oxford Nanopore raw data was obtained from SRA id SRR10032546 using command bellow:

fastq-dl SRR10032546

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

## Trimmomatic was used to remove bad reads and adapters from Illumina data


**INSTALLATION**

Conda

conda create --name trimmomatic-env -c conda-forge -c bioconda trimmomatic

**USAGE**

trimmomatic PE -phred33 SRR1797886_1.fastq SRR1797886_2.fastq SRR1797886_1_paired.fastq SRR1797886_1_unpaired.fastq SRR1797886_2_paired.fastq SRR1797886_2_unpaired.fastq ILLUMINACLIP:TruSeq3-PE.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36

## spades was used to assemble genome only with illumina NGS data

**INSTALLATION**

Conda

conda create --name spades-env -c conda-forge -c bioconda spades


**USAGE**

spades.py --pe1-1 SRR1797886_1_paired.fastq --pe1-2 SRR1797886_2_paired.fastq --pe1-s SRR1797886_1_unpaired.fastq --pe1-s SRR1797886_2_unpaired.fastq -o illumina_assemble

## BUSCO and QUAST were used to evaluate genome assembly 

**INSTALLATION**

Conda

conda create --name busco-env -c conda-forge -c bioconda busco

conda create --name quast-env -c conda-forge -c bioconda quast


**USAGE**


