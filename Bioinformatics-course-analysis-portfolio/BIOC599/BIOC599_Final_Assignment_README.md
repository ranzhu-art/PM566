# BIOC 599 Final Project: Genomic and Epigenomic Data Analysis

## Overview

This project presents a set of bioinformatics analyses completed as part of BIOC 599. The work covers four major sequencing applications:

- RNA-seq alignment and differential expression analysis
- ChIP-seq signal processing and peak calling
- ATAC-seq peak characterization and motif enrichment
- Nanopore long-read methylation and haplotype analysis

The project combines command-line workflows, R-based statistical analysis, high-performance computing, and genome-browser visualization. Course prompts, restricted datasets, answer documents, and user-specific server paths are not included in this repository.

## Project Components

### 1. RNA-seq Analysis

The RNA-seq workflow evaluated how alignment methods affect downstream results and examined differential gene expression after 5-AZA treatment.

#### Workflow

1. Performed quality-score trimming.
2. Aligned paired-end reads to the hg38 reference genome using STAR and HISAT2.
3. Compared post-alignment quality-control metrics, including alignment rate, uniquely mapped pairs, singleton reads, genome coverage, and coverage depth.
4. Quantified gene expression using a GENCODE annotation.
5. Applied median-ratio normalization and differential expression analysis with DESeq2.
6. Filtered differentially expressed genes using FDR < 0.05 and an absolute fold-change threshold greater than 2.
7. Generated a volcano plot and examined affected biological pathways using Ingenuity Pathway Analysis.

#### Selected Results

- HISAT2 completed alignment faster than STAR for the analyzed dataset.
- STAR produced substantially fewer uniquely mapped singleton reads, supporting its use for the paired-end analysis.
- In the 10 µM versus 0 µM comparison, 501 genes were upregulated and 207 genes were downregulated under the selected thresholds.
- Several interferon-response and cell-cycle pathways were enriched after treatment.

### 2. ChIP-seq Analysis

The ChIP-seq workflow converted raw sequencing reads into genome-aligned signal tracks and identified enriched genomic regions.

#### Workflow

1. Aligned reads to hg38 using BWA.
2. Converted, sorted, and assessed BAM files using SAMtools.
3. Marked duplicate reads using Picard.
4. Generated tag directories and bedGraph signal files with HOMER.
5. Converted bedGraph output to bigWig format for genome-browser visualization.
6. Called peaks against an input control using MACS2.
7. Generated signal matrices and heatmaps with deepTools.
8. Clustered peak-centered signal profiles using k-means.
9. Visualized ChIP-seq signal tracks and genomic annotations in IGV.

#### Selected Results

- Approximately 4.94 million reads mapped to hg38 in the primary analysis.
- MACS2 identified 43,362 candidate enriched regions using the specified permissive threshold.
- Peak-centered heatmaps separated regions into four signal-pattern clusters.
- IGV visualization showed a concentrated signal near the transcription start site of the SKIL gene.

An additional analysis of public ZFX ChIP-seq data compared two biological replicates, identified 11,556 overlapping peaks, and visualized shared signal patterns across promoter, gene-body, and intergenic regions.

### 3. ATAC-seq Analysis

The ATAC-seq workflow characterized accessible chromatin peaks and compared them with an external ENCODE peak set.

#### Workflow

1. Inspected ATAC-seq peaks in IGV.
2. Calculated peak-length summary statistics in R.
3. Filtered significant peaks using q-value < 0.01.
4. Examined the relationship between peak size and statistical significance.
5. Measured peak overlap with an ENCODE narrowPeak dataset using BEDTools.
6. Performed known-motif enrichment analysis using HOMER.

#### Selected Results

- The peak set had a mean length of approximately 313 bp.
- A total of 290 peaks passed the q-value threshold.
- BEDTools identified 175 peaks overlapping the selected ENCODE reference set.
- Forkhead-family motifs, including FOXA1, FOXA2, and FOXA3 motifs, were among the most significantly enriched known motifs.

### 4. Nanopore Long-Read Methylation Analysis

The long-read workflow examined DNA methylation and haplotype-specific patterns in HG002 Nanopore data.

#### Workflow

1. Ran the NANOME workflow with Nextflow and Apptainer.
2. Performed methylation detection and haplotype phasing.
3. Extracted methylation measurements for selected genomic regions.
4. Compared HP1 and HP2 methylation levels in R.
5. Visualized methylation distributions with boxplots.
6. Inspected haplotype-specific CpG methylation patterns in IGV.

#### Selected Results

- The workflow generated methylation results for HP1, HP2, and combined reads.
- The selected regions showed varying levels of haplotype-specific methylation.
- One examined region displayed a large methylation difference between HP1 and HP2, whereas another showed relatively similar methylation levels between haplotypes.

## Tools and Technologies

| Category | Tools |
| --- | --- |
| Programming and statistics | R, DESeq2 |
| Alignment and BAM processing | STAR, HISAT2, BWA, SAMtools, Picard |
| Peak and motif analysis | MACS2, HOMER, BEDTools |
| Signal visualization | deepTools, IGV, UCSC bedGraphToBigWig |
| Workflow and containers | Nextflow, Apptainer |
| Computing environment | Linux, SLURM |
| Reference resources | hg38, GENCODE, ENCODE |

## Suggested Repository Structure

```text
BIOC599-final-project/
├── README.md
├── rnaseq/
│   ├── scripts/
│   └── figures/
├── chipseq/
│   ├── scripts/
│   └── figures/
├── atacseq/
│   ├── scripts/
│   └── figures/
└── nanopore-methylation/
    ├── scripts/
    └── figures/
```

## Data Availability

Raw sequencing files are not distributed in this repository because of file-size and access restrictions. Public accession numbers or download instructions should be provided within the relevant analysis folders when redistribution is permitted.

## Reproducibility Notes

- Replace all user-specific cluster paths with configurable variables before running the workflows.
- Confirm that the hg38 reference genome, annotation release, and chromosome-size files are compatible.
- Record software versions and computing resources for each analysis.
- Do not commit FASTQ, BAM, bigWig, or other large generated files directly to GitHub.
- Do not upload credentials, tokens, restricted course materials, or unpublished research data.

## Author

Ran Zhu  
M.S. Student in Translational Biomedical Informatics  
University of Southern California

## Disclaimer

This repository is a portfolio-oriented summary of independently completed analytical work. It does not reproduce the original course questions, grading materials, restricted input data, or full submitted assignment.
