# Microbiota analysis - Asthma and Obesity

## Quality control analysis before and after trimming/clipping

$ fastqc -o fastqc *.fastq

$ multiqc fastqc

BEFORE:
https://rawcdn.githack.com/Microbial-Ecosystems-Lab/asthma_obesity/main/multiqc_report.html

AFTER:
https://rawcdn.githack.com/Microbial-Ecosystems-Lab/asthma_obesity/3cfe0d18e96491b26cf1067e031757893af98d52/multiqc_report_filtered.html

# Taxonomy database

https://zenodo.org/records/4587955#.YfxAfOrMI2w

# Custom database - Refseq NCBI 16S sequences

All sequences' ID were downloaded from NCBI (see file IDs_16Ssequences.txt).

To download the sequences we used edirect 

$ split -l 1000 IDs_16Ssequences.txt 

$ for i in `ls x*`; do epost -db nuccore -input ${i} -format acc | efetch -format fasta > ${i}.fasta; done

$ cat *.fasta > 16Ssequences.fasta

# Full lineage annotation

$ ftp://ftp.ncbi.nlm.nih.gov/pub/taxonomy/taxdump.tar.gz

See script get_lineage.ipynb

# Filter quality and length

Nanofilt

$ 
