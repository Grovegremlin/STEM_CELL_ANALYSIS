# GSE182158 Pseudobulk Analysis

This repository contains a Jupyter notebook (`analysis_1.ipynb`) for processing single-cell RNA-seq data from the GEO dataset GSE182158 into pseudobulk format.

## Data Source

The data is from the public Gene Expression Omnibus (GEO) repository.

- **GEO Accession:** [GSE182158](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE182158)

## Description

The primary goal of this project is to take raw single-cell RNA-sequencing data, perform comprehensive quality control, and aggregate the cell-level expression data into donor-level "pseudobulk" profiles. This aggregated format is often used for analyses that require sample-level data, such as differential expression analysis across donor groups.

## Workflow

The `analysis_1.ipynb` notebook performs the following key steps:

1.  **Setup and Dependencies**: Imports required Python libraries like `scanpy`, `pandas`, and `matplotlib`, and sets up the environment.
2.  **Data Download and Extraction**: Downloads the supplementary raw data from GEO, extracts the main archive, and recursively expands any nested archives to locate the 10x Genomics files.
3.  **Data Restructuring**: Reconstructs standard 10x Genomics directories (`matrix.mtx`, `barcodes.tsv`, `features.tsv`) from flat file layouts if necessary.
4.  **Quality Control (QC)**: Implements a multi-stage QC process to identify and flag low-quality cells. This includes:
    *   Calculating basic metrics (total UMI counts, number of genes per cell).
    *   Analyzing the percentage of mitochondrial gene expression.
    *   Applying a sophisticated power-law envelope filter to remove cells with high mitochondrial content relative to their library size.
5.  **Data Loading**: Loads the valid 10x data into `AnnData` objects for analysis with `scanpy`.
6.  **Pseudobulk Aggregation**: Groups cells by donor and tissue type to sum their counts, creating a pseudobulk expression matrix.
7.  **Normalization**: Applies Counts Per Million (CPM) normalization and a log transformation to the pseudobulk data.
8.  **Export Results**: Saves the final processed pseudobulk matrix, metadata, and panel information into various formats (`.csv`, `.h5ad`) for downstream use.
