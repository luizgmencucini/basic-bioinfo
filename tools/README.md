## fastq-dl was used to download raw genomic data from SRA or ENA

**INSTALLATION**

Conda
conda create --name fastq-dl-env -c conda-forge -c bioconda fastq-dl


**USAGE**

First, activate conda env created before:
conda activate fastq-dl-env 


for help:
https://github.com/rpetit3/fastq-dl

In this example, we try to assemble and annotate Actinomadura madurae genome
Raw data was obtained from SRA id SRR18463445 using command bellow:
fastq-dl SRR18463445


** UNTAR ARCHIVES**

gunzip SRR18463445_1.fastq.gz 

## fastqc was used to check raw genomic data quality
**INSTALLATION**

Conda
conda create --name fastqc-env -c conda-forge -c bioconda fastqc


**USAGE**

Activating fastqc environment:

conda activate fastqc-env

## Trimmomatic was used to remove bad reads and adapters

**INSTALLATION**

Conda
conda create --name trimmomatic-env -c conda-forge -c bioconda trimmomatic


**USAGE**

## spades was used to assemble genome

**INSTALLATION**

Conda
conda create --name spades-env -c conda-forge -c bioconda spades


**USAGE**
