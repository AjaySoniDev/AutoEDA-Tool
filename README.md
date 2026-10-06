<h1 align="center">AutoEDA-Tool</h1>

<p align="center">
  <strong>Interactive R Shiny application for focused exploratory data analysis.</strong><br>
  Upload a CSV, choose analysis tasks, inspect summaries, visualize numeric relationships, detect IQR-based outliers, review data types, and calculate pairwise correlations.
</p>

<p align="center">
  <img alt="Status" src="https://img.shields.io/badge/status-working%20prototype-blue">
  <img alt="R" src="https://img.shields.io/badge/language-R-276DC3">
  <img alt="Framework" src="https://img.shields.io/badge/framework-Shiny-informational">
  <img alt="Visualization" src="https://img.shields.io/badge/visualization-ggplot2-orange">
  <img alt="License" src="https://img.shields.io/badge/license-MIT-green">
</p>

<p align="center">
  <a href="#overview">Overview</a> ·
  <a href="#what-this-repo-contains">Contents</a> ·
  <a href="#features">Features</a> ·
  <a href="#architecture">Architecture</a> ·
  <a href="#run-locally">Run Locally</a>
</p>

---

## Overview

**AutoEDA-Tool** is a single-file R Shiny prototype for interactive exploratory data analysis.

A user uploads a CSV, selects one or more EDA tasks, and launches an analysis session. The application then creates task-specific controls and outputs dynamically.

~~~text
CSV upload
   ↓
Select EDA tasks
   ↓
Load dataset with read.csv
   ↓
Choose columns / actions
   ↓
Generate tables and plots
~~~

The implementation is intentionally transparent and educational rather than a full automated profiling platform.

---

## What This Repo Contains

| File | Purpose |
|---|---|
| <code>script.R</code> | Complete Shiny UI, server logic, helper functions, styling, and analysis workflow. |
| <code>data.csv</code> | Sample CSV data for local experimentation. |
| <code>distribution.jpg</code> | Example visual asset. |
| <code>README.md</code> | Project documentation. |
| <code>LICENSE</code> | MIT License. |

---

## Features

| Area | Current Implementation |
|---|---|
| CSV ingestion | Shiny <code>fileInput</code> restricted to <code>.csv</code>. |
| Task selection | Checkbox-driven plotting, summaries, outliers, data types, correlations, and distributions. |
| Summary statistics | Min, median, mean, max, standard deviation, variance, and missing-value counts for selected columns. |
| Histograms | Base-R histograms for a selected feature. |
| Scatter plots | Base-R two-column scatter plots. |
| Outlier analysis | IQR rule using Q1/Q3 plus a ggplot2 boxplot. |
| Data types | Column names and R classes. |
| Correlation | Pairwise Pearson correlation through <code>cor(..., use="complete.obs")</code>. |
| Distribution view | ggplot2 density plot for a selected feature. |
| Reload | Session reload button for restarting the analysis. |
| Styling | Embedded visual styling inside <code>script.R</code>. |

---

## User Flow

~~~text
Open Shiny app
   ↓
Upload CSV
   ↓
Choose EDA tasks
   ↓
Click START ANALYSIS
   ↓
Select columns for each enabled task
   ↓
Generate plots / tables
   ↓
Reload when a clean session is needed
~~~

---

## Architecture

~~~text
script.R
├── Analysis helpers
│   ├── summary_fn()
│   ├── outlier_fn()
│   ├── total_outlier()
│   ├── dist_fn()
│   ├── data_fn()
│   └── correlation_fn()
├── Shiny UI
│   ├── upload controls
│   ├── task selector
│   ├── dynamic analysis controls
│   └── embedded CSS
└── Shiny server
    ├── CSV loading
    ├── reactive task rendering
    ├── plot/table generation
    └── session reload
~~~

The app keeps analysis state inside the Shiny session and does not use an external database or backend service.

---

## Repository Structure

~~~text
AutoEDA-Tool/
├── script.R
├── data.csv
├── distribution.jpg
├── README.md
└── LICENSE
~~~

---

## Run Locally

Install the two declared libraries:

~~~r
install.packages("shiny")
install.packages("ggplot2")
~~~

Run:

~~~r
shiny::runApp("script.R")
~~~

RStudio users can also open <code>script.R</code> and use **Run App**.

---

## Validation & Current Maturity

AutoEDA-Tool is best described as a **working educational prototype**.

Current strengths include an inspectable EDA pipeline, dynamic task-specific controls, and no hidden server dependency.

Current engineering limits:

- no automated test suite;
- no <code>renv.lock</code> or other dependency lock;
- monolithic single-file application;
- numeric plotting/correlation functions assume compatible numeric columns rather than enforcing a comprehensive schema;
- no downloadable profiling report;
- no claim of production statistical validation.

---

## Important Notes

- CSV upload is the implemented ingestion path.
- Correlation and numeric plots should be used with numeric features.
- IQR outlier flags are heuristics; they do not prove that a value is erroneous.
- Summary statistics and plots describe the uploaded data only and do not establish causal relationships.

---

## License

Released under the **MIT License**. See <code>LICENSE</code>.
