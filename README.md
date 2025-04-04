# N-of-1 HOMDD Studies TAU-U Analysis

## Overview
This repository contains comprehensive analysis code for analyzing the N-of-1 study data, i.e., the TAU-U statistical test for evaluating the treatment effects on the primary and secondary clinical outcome measures and the Protein Expression Analysis for studying the corresponding plasma protein expression patterns. The project includes both statistical evaluation of treatment outcomes and proteomics data analysis.

## Project Structure
```
N-of-1-HOMDD-1-Studies-TAU-U-Analysis/
├── 0_PatK_stats.R        # Patient K statistical analysis
├── 1_PatK_protexpr.R     # Patient K protein expression analysis
├── All_identified_proteins_PatK_filtered_norm.csv  # Patient K data
├── data.xlsx             # TAU-U treatment data
└── README.md            # This documentation
```

## Protein Expression Analysis

### Data Structure
The protein expression data is stored in CSV files with the following columns:
- `Accession`: Protein accession number
- `Peptide count`: Number of peptides identified
- `Unique peptides`: Number of unique peptides
- `Confidence score`: Score indicating protein identification confidence
- `Anova (p)`: ANOVA p-value for expression changes
- `q Value`: Adjusted p-value for multiple testing
- `Max fold change`: Maximum fold change in expression
- `Power`: Statistical power of the measurement
- `Highest mean condition`: Time point with highest mean expression
- `Lowest mean condition`: Time point with lowest mean expression
- `Mass`: Protein molecular mass
- `Description`: Protein description including gene name
- Multiple columns for expression measurements at different time points (W2, W4, W8, etc.)

### Analysis Scripts

#### 1. Statistical Analysis (0_PatK_stats.R)
- Performs initial statistical analysis of protein expression data
- Conducts ANOVA and multiple testing corrections
- Identifies significant changes in protein expression

#### 2. Protein Expression Analysis (1_PatK_protexpr.R)
- Analyzes protein expression patterns over time
- Creates visualizations including heatmaps
- Compares treatment vs placebo conditions

## TAU-U Treatment Effect Analysis

### About TAU-U
To analyze the primary and secondary outcome measures of the N-of-1 trial, we used the Tau-U statistical test (Parker et al. 2011), a popular single-case non‐parametric effect size estimator that is not significantly influenced by the degree of autocorrelation. Tau-U is a non-parametric, distribution-free method suitable for small datasets. It assesses the nonoverlap between the treatment phases, controlling for the time series trend within the intervention phase (Barnard-Brak et al., 2021). Here, we provide the R statistical programming language for the TAU-U calculation.

### Data Requirements
- Excel file containing treatment period data
- Columns: Treatment Period, PCS, MCS, BDI

### Statistical Methods
The analysis uses the `SingleCaseES` package to perform:
- Tau-U analysis (Parker's method)
- Linear regression for trend analysis
- Confidence interval calculations

### Visualizations
- Line plots for PCS, MCS, and BDI over time
- Faceted plots by treatment period
- Linear trend lines with confidence intervals

## Setup and Installation

### Required R Packages
```R
install.packages(c(
  "data.table",
  "ggplot2",
  "ggrepel",
  "pheatmap",
  "stringr",
  "readxl",
  "tidyverse",
  "scan",
  "kableExtra",
  "SingleCaseES",
  "pacman"
))
```

### Project Setup
1. Install all required R packages using the command above
2. Place the data files in their respective locations:
   - Protein expression data: `All_identified_proteins_PatK_filtered_norm.csv`
   - TAU-U data: `data.xlsx`

## Usage

### Protein Expression Analysis
1. Ensure all required R packages are installed
2. Place the data files in the specified directory
3. Run the analysis scripts in sequence:
   ```R
   # First run the statistics scripts
   source("0_PatK_stats.R")
   
   # Then run the protein expression analysis
   source("1_PatK_protexpr.R")
   ```

### TAU-U Analysis
1. Ensure the Excel data file is properly formatted
2. Run the TAU-U analysis code:
   ```R
   # Load required packages
   pacman::p_load(tidyverse, scan, kableExtra, SingleCaseES)
   
   # Read data
   data <- read_excel("data.xlsx")
   
   # Run TAU-U analysis
   # (See code in README.md for complete analysis)
   ```

## Results Interpretation

### Protein Expression
- Significant changes in protein expression are identified using ANOVA and multiple testing corrections
- Heatmaps show expression patterns across different time points
- Treatment vs placebo comparisons highlight potential treatment effects

### TAU-U Outcomes
- Tau-U values indicate treatment effect size
- Confidence intervals provide statistical significance
- Visualizations show trends in PCS, MCS, and BDI scores

### References
- Parker RI, Vannest KJ, Davis JL, Sauber SB. Combining Nonoverlap and Trend for Single-Case Research: Tau-U. Behav Ther [Internet]. 2011 Jun;42(2):284–99. Available from: https://linkinghub.elsevier.com/retrieve/pii/S0005789411000153
- Barnard-Brak L, Watkins L, Richman DM. Autocorrelation and estimates of treatment effect size for single-case experimental design data. Behavioral Interventions. 2021 Jul 1;36(3):595–605.

## Contact
For questions about the analysis or data, please contact the project maintainer.

