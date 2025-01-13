:: **Course of Genomic Data Analysis** :: 

**1. STEP: DATA COLLECTION  NCBI**

Primeiro vamos fazer o download do genoma de referência do *C. elegans* usando o link:

[Genome assembly WBcel235reference](https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_000002985.6/)

Usar o comando exibido pelo link acima, na aba datasets:

$ datasets download genome accession GCF_000002985.6 --include gff3,rna,cds,protein,genome,seq-report

Extrair os arquivos:

$ unzip ncbi_dataset.zip

"The complete example of downloading the reference genome is following:"
# create and move to directory for reference genome
mkdir ref
cd ref

# download genome using NCBI datasets command line tools
# docs - https://www.ncbi.nlm.nih.gov/datasets/docs/v2/reference-docs/command-line/datasets/download/genome/
# reference genome - https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_000002985.6/

datasets download genome accession GCF_000002985.6 --assembly-level complete --reference --assembly-source RefSeq
unzip ncbi_dataset.zip

# move to the directory containing actual data
cd ncbi_dataset/data/GCF_000002985.6/
ls
# View data and verify a file such as "GCF_000002985.6_WBcel235_genomic.fna" is present

# view initial contents of FASTA file
head -5 GCF_000002985.6_WBcel235_genomic.fna

# verify that your genome has same number of chromosomes as the actual shown
more GCF_000002985.6_WBcel235_genomic.fna | grep ">" | wc -l
# 7 
# check how many chromosomes does the reference genome (following link) has? 
# https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_000002985.6/#:~:text=19%2C972-,Chromosomes,-I

# copy the reference genome to ref for easy access
cp GCF_000002985.6_WBcel235_genomic.fna ../../../

# move to parent directory of ref for next steps
cd ../../../../


**2. STEP: SRA-Toolkit**


$ docker pull ncbi/sra-tools


OR


$ mkdir reads
$ cd reads

# after running following command, you will get a file with .sra command
$ prefetch SRR27482193 

# convert .sra to .fastq
$ cd SRR27482193
$ fasterq-dump -v SRR27482193.sra

# See the new contents of the directory
$ ls
# you can move back to your working directory if you following along
$ cd ../../
