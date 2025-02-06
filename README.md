# Snakemake-RNAseq

This is a snakemake pipeline for RNA sequencing data analysis for LAIDD project

## Dependencies
The following software and Python libraries are required:

- **Snakemake**: Workflow management system
- **Cutadapt**: Read trimming tool
- **FastQC & MultiQC**: Quality control tools
- **STAR or HISAT2**: RNA-seq read alignment tools
- **Samtools**: BAM file processing utilities
- **featureCounts**: Gene quantification tool
- **Python**: Required for Snakemake execution
- **Pandas & NumPy**: For sample data processing

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


# Usage
In RNA-seq data processing workflows, the number of threads (or CPU cores) used for various tools can have a significant impact on the speed and efficiency of the analysis. This can be controlled by adjusting the threads option in the config.yaml file. 

It is recommended that the number of cores allocated to Snakemake (--cores option) is higher than the number of threads specified in the config.yaml file. This ensures that Snakemake has enough resources to handle multiple rules or jobs in parallel, thus improving overall performance.



## Pipeline Structure
The pipeline consists of the following Snakemake rules:
![image](https://github.com/user-attachments/assets/74d10d59-1b0f-4d77-933e-df27342725b5)

### 1. `rule all`
Defines the final output, ensuring that gene quantification and quality control reports are successfully generated.
- **Output Files**:
  - `merged.gene.txt`: Final merged gene expression matrix
  - `qc_files.done`: Quality control completion marker

### 2. `all_samples`
Extracts the list of sample names from `samples.tsv`, ensuring that all required samples are processed.

### 3. `format_options(options)`
Formats optional command-line arguments into a single string for command execution.

## Configuration
The `config.yaml` file should specify input paths, output directories, and analysis options. Example:

```yaml
samples: "samples.tsv"
path:
  default: "./data"
```

## Included Rules
The pipeline includes additional Snakemake rule files:
- `rules/cutadapt.smk`: Read trimming and adapter removal
- `rules/qc.smk`: Quality control analysis
- `rules/alignment.smk`: Read alignment to reference genome
- `rules/quantification.smk`: Gene quantification using featureCounts
  
# Setup
Create conda environment.
```
conda env create -f environment.yaml
```
## Execution
After finishing the setup, inside the repo's base directory with Snakefile do a dry run to check for errors
```
snakemake -n
````
Once you're ready to run the analysis type
```bash
snakemake --cores <num_cores>
```
Replace `<num_cores>` with the number of available CPU cores.

## Output Files
- **Gene Expression Data**: `merged.gene.txt`
- **Quality Control Reports**: `qc_files.done`
- **Log Files**: Stored in `log_dir`

## Troubleshooting
- Ensure `config.yaml` contains correct paths and options.
- Verify `samples.tsv` has the correct format with a `SAMPLE_ID` column.
- Check `log_dir` for error messages.
- Ensure required tools (Cutadapt, STAR, Samtools, featureCounts) are installed and properly configured.

## Author
This pipeline was developed for RNA-seq quantification and quality control using Snakemake.

For inquiries, please contact the developer or refer to the relevant tool documentation.





