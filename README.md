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

OBS.: "NR_181206.1" "NR_179899.1" "NR_177715.1" "NR_177711.1" "NR_074799.1" "NR_172695.1" "NR_157681.1" "NR_074597.1" "NR_028866.1"
      "These RefSeqs records were removed because data validation identified problems with the assembly or annotation". 

# TaxID database

Step necessary to link Refseq access number to a full lineage annotation

$ wget https://ftp.ncbi.nlm.nih.gov/pub/taxonomy/new_taxdump/new_taxdump.tar.gz

$ tar -zxvf new_taxdump.tar.gz

See script 2-Parsing_Database_Refseq16S.ipynb

# Reference alignment

Using KMA-1.3.23 - Clausen, Aarestrup & Lund. Rapid and precise alignment of raw reads against redundant databases with KMA. BMC Bioinformatics, 19, 307 (2018).

$ kma index -i 16Ssequences.fasta -o 16sequences_index_kma/16Ssequences

$ kma -i ${i}.fastq -o output_16s_refseq/${i}_kma -t_db 16sequences_index_kma/16Ssequences -bcNano -bc 0.7



