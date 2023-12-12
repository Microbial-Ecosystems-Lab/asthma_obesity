# Microbiota analysis - Asthma and Obesity

## Quality control analysis before and after trimming/clipping

$ fastqc -o fastqc *.fastq

$ multiqc fastqc

BEFORE:
https://rawcdn.githack.com/Microbial-Ecosystems-Lab/asthma_obesity/main/multiqc_report.html

AFTER:
https://rawcdn.githack.com/Microbial-Ecosystems-Lab/asthma_obesity/3cfe0d18e96491b26cf1067e031757893af98d52/multiqc_report_filtered.html

# Filter quality and length

See script 1-Preprocessing.ipynb

# Custom database - Refseq NCBI 16S sequences

All sequences' ID were downloaded from NCBI (see file IDs_16Ssequences.txt).

To download the sequences we used edirect 

$ split -l 1000 IDs_16Ssequences.txt 

$ for i in `ls x*`; do epost -db nuccore -input ${i} -format acc | efetch -format fasta > ${i}.fasta; done

$ cat *.fasta > 16Ssequences.fasta

# Reference alignment

Using KMA-1.3.23 - Clausen, Aarestrup & Lund. Rapid and precise alignment of raw reads against redundant databases with KMA. BMC Bioinformatics, 19, 307 (2018).

$ kma index -i 16Ssequences.fasta -o 16sequences_index_kma/16Ssequences

$ kma -i ${i}.fastq -o output_16s_refseq/${i}_kma -t_db 16sequences_index_kma/16Ssequences -bcNano -bc 0.7

# Taxonomy annotation

Taxonomy database

$ wget https://ftp.ncbi.nlm.nih.gov/pub/taxonomy/new_taxdump/new_taxdump.tar.gz

$ tar -zxvf new_taxdump.tar.gz

See script 2-AssignTaxonomy_Refseq16S.ipynb

