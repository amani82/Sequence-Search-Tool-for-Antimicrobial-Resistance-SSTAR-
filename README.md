# Manual for Sequence Search Tool for Antimicrobial Resistance (SSTAR), version 1.0

## Introduction

SSTAR enables fast and accurate antimicrobial resistance (AR) surveillance from Whole Genome Sequencing (WGS) data. It is able to identify known AR genes and detect putative new variants as well as truncated genes due to internal stop codons. 
SSTAR also reports modifications and/or truncations in outer membrane porins.

## Obtaining and installing SSTAR dependencies

SSTAR combines a standalone BLASTN with a Java interface, which operates under Windows and Unix systems. 
In order to run SSTAR you need Java 1.6 or higher and standalone BLAST 2.2.29+ or BLAST 2.2.30+ installed on your system. 

### For Windows users:
BLAST+ needs to be installed in C:\\Program Files\\NCBI\\blast-2.2.29+ or C:\\Program Files\\NCBI\\blast-2.2.30+, which are the default locations after following the BLAST installation steps in the installation wizard.

### For OS X and Linux users:
BLAST+ needs to be installed in /usr/local/ncbi/blast/bin. One can also place links in /usr/local/ncbi/blast/bin using the “ln –s” command if BLAST+ is installed elsewhere.

### For all users:
Java can be downloaded from the ORACLE website at: https://java.com/en/download/index.jsp

A BLAST+ copy and easy installation guide of standalone BLAST can be retrieved from: http://www.blaststation.com/freestuff/en/howtoNCBIBlastWin.html

**SSTAR is available as an executable JAR file, however the raw java file is available too. The java source file needs to be compiled into a class file before using.
In the downloaded archive you will find three different SSTAR versions. SSTAR is for Linux and OS X, SSTAR_win_29 is for Windows systems with BLAST 2.2.29+ and SSTAR_win_30 is for Windows systems with BLAST 2.2.30+. 
SSTAR was successfully tested under Windows 7, OS X 10.9.5 and Ubuntu 14.04 LTS.**

## Input data
One needs two input files in order for SSTAR to run: A microbial genome assembly and AR gene file, both in FASTA format. SSTAR is developed in a certain way so it can handle the ‘SRST2 ARG-ANNOT database header’ format. 
This format is specified below.

### The AR gene file header format:

The format of each AR gene FASTA header is structured like the below example:

**92__CMY_Bla__CMY-37__402**

The AR gene family is between the first and second double underscore (CMY_Bla) and the variant is between the second and third double underscore (CMY-37).
The first number (92) is a unique identifier for each AR gene group. The last number (402) is a unique identifier for each single variant. The other information in the header (right of the space) is ignored by SSTAR and not shown in this manual example.

Users who want to use different AR databases (ResFinder or custom databases) need to make sure the headers have the exact same structure as the SRST ARG-ANNOT header format. 

## Running SSTAR
SSTAR contains an easy interface with currently only four buttons. The top two buttons are for uploading the genome assembly file and the AR gene database file. Both files need to be in FASTA format. 
The ‘Identify resistance genes’ button starts the actual AR gene annotation process. The output will appear in the top right output window.

### AR gene output
The top right output window displays the AR resistance genes and porins that are identified on your input genome assembly. Each output line contains four fields, separated by a tab:

1.	The AR gene name
2.	The contig, scaffold or chromosome where the AR gene is located
3.	Alignment length
4.	AR gene length

First, SSTAR lists the potential new alleles or variants at the top of the window. These are the variants that share between 95 and 99.99% sequence similarity with an AR gene in the used database. 
Below the potential new variants SSTAR lists the AR genes that share 100% sequence similarity with AR genes in the used database. The alignment length shows the user how much of the AR database gene is found on your genome. In other words, when the alignment length equals the gene length one identified the full AR gene with 100% sequence similarity. 

### Detecting new and truncated AR gene variants
The bottom left output window will show putative new variants and truncated enzymes in protein space. The protein sequences can be exported to a plain text file using the “Export potentially new enzyme(s)” button. The file is saved in the same directory as the input genome assembly file. 
The protein file can be used with BLASTP against the NR database of NCBI for detecting new variants. Beta-lactamase proteins can be send to the Lahey website (http://www.lahey.org/Studies/) for verification. 
When a protein sequence contains an internal stop codon it will be flagged underneath the FASTA header of that particular protein. This makes the FASTA file invalid and forces the user to remove that sequence from the file. Protein sequences with internal stop codons are otherwise easily missed and misinterpreted as putative new variants of an AR gene group.

### Detecting modified and truncated outer membrane variants
The bottom left output window will also show modified and/or truncated outer membrane porins (OMPs). We have included OmpK35 and OmpK36 from Klebsiella pneumoniae, OmpC and OmpF from Escherichia coli, OmpC and OmpF from Enterobacter cloacae and Omp35 and Omp36 from Enterobacter earogenes. 
When a porin protein sequence contains an internal stop codon it will be flagged underneath the FASTA header of that particular porin as truncated. 

## Citing SSTAR
Manuscript in progress

## Contact 
For assistance, feedback or suggestions please contact Tom de Man via xku6@cdc.gov or tjb.deman@gmail.com
 



