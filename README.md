# Snakemake-RNAseq

This is a snakemake pipeline for RNA sequencing data analysis for LAIDD project

# References

You'll need a reference genome. The GRCh38 (hg38) genome is available on the Broad's GATK [website](https://gatk.broadinstitute.org/hc/en-us/articles/360035890811-Resource-bundle), GTF files(GRCh38.112) [ensembl.org](https://ftp.ensembl.org/pub/release-112/gtf/homo_sapiens/)

# Adapter Sequences for Cutadapt
In addition to preparing the reference genome and annotations for RNA-seq analysis, it is important to ensure that the correct adapter sequences are identified for trimming your raw sequencing reads using cutadapt. Adapter sequences are often added during the sequencing library preparation process and need to be removed before alignment for accurate results.

# Setup
Create conda environment.
```
conda env create -f environment.yaml
```

