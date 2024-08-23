# Snakemake-RNAseq

This is a snakemake pipeline for RNA sequencing data analysis for LAIDD project

# References

You'll need a reference genome. The GRCh38 (hg38) genome is available on the Broad's GATK [website](https://gatk.broadinstitute.org/hc/en-us/articles/360035890811-Resource-bundle), GTF files(GRCh38.112) [ensembl.org](https://ftp.ensembl.org/pub/release-112/gtf/homo_sapiens/)

## Generate STAR genome Index

```
STAR --runMode genomeGenerate \
     --genomeDir reference_genome_GC \
     --genomeFastaFiles Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa \
     --sjdbGTFfile Homo_sapiens.GRCh38.112.gtf \
     --runThreadN 8
```

# Adapter Sequences for Cutadapt
In addition to preparing the reference genome and annotations for RNA-seq analysis, it is important to ensure that the correct adapter sequences are identified for trimming your raw sequencing reads using cutadapt. Adapter sequences are often added during the sequencing library preparation process and need to be removed before alignment for accurate results.

# Setup
Create conda environment.
```
conda env create -f environment.yaml
```
# Usage
After finishing the setup, inside the repo's base directory with Snakefile do a dry run to check for errors

In RNA-seq data processing workflows, the number of threads (or CPU cores) used for various tools can have a significant impact on the speed and efficiency of the analysis. This can be controlled by adjusting the threads option in the config.yaml file. 

It is recommended that the number of cores allocated to Snakemake (--cores option) is higher than the number of threads specified in the config.yaml file. This ensures that Snakemake has enough resources to handle multiple rules or jobs in parallel, thus improving overall performance.
```
snakemake -n
````
Once you're ready to run the analysis type

```
snakemake -j [cores]
```





