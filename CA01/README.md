# CA01 — Exploratory Data Analysis (EDA): House Price Dataset

This repository contains a Jupyter Notebook that performs **Exploratory Data Analysis (EDA)** and **data cleaning** on the Ames Housing training dataset (`house-price-train.csv`) in preparation for future machine learning modeling. The notebook follows the three-part structure required in the assignment: **(1) Data Understanding + Data Quality Report**, **(2) Data Cleaning**, and **(3) Collinearity Visualization + Feature Selection**. 

---

## Dataset

The analysis uses the provided **training dataset**:

- `house-price-train.csv` — training data used for EDA and cleaning  
- `data_description.txt` — data dictionary describing feature meanings and codes

> Note: The assignment specifies using the **training file only** for this submission and producing all work directly inside the notebook (no separate report). 

---

## Notebook Overview (What Was Done)

### Part 1 — Data Understanding & Data Quality Report
The notebook begins by loading the dataset and building an understanding of:

- Dataset shape and feature types (numeric vs categorical)
- Distribution and characteristics of the target (`SalePrice`)
- Univariate and bivariate patterns (including relationships with `SalePrice`)
- A **Data Quality Report (DQR)** that identifies key issues:
  - Missing values (counts and percentages)
  - Structural missingness vs true missingness (based on the data dictionary)
  - Duplicate rows
  - Potential outliers
  - Initial correlation signal with the target

This matches the assignment requirement that Part 1 output includes visual variable analysis and ends in a **Data Quality Report identifying data problems**. 

---

### Part 2 — Data Cleaning (Fixing Issues Found in the DQR)
Using the problems identified in Part 1, the notebook performs targeted cleaning:

#### Missing Values (Structural vs True Missingness)
Many features use `"NA"` to represent **absence of a feature**, not unknown values (e.g., `Alley`, `PoolQC`, `Fence`, `MiscFeature`, basement and garage-related fields). These were treated as **structural missingness** and filled with appropriate placeholders such as `"None"` (categorical) or `0` (numeric) where applicable. 

True missingness (e.g., `LotFrontage`) was imputed using sensible strategies (e.g., neighborhood-based medians) to preserve locality effects.

#### Outlier Treatment
The notebook flags large outliers in continuous area-related variables (e.g., lot size and square footage) and applies a consistent strategy to reduce undue influence on downstream analysis (e.g., winsorization/capping using IQR-based thresholds), while preserving all rows.

At the end of Part 2, missing values are re-checked and the dataset is validated as “analytics ready.”

---

### Part 3 — Collinearity & Feature Selection (Multicollinearity)
Part 3 focuses only on **collinearity visualization** and **identifying redundant features** for potential removal (feature selection), as required by the assignment. Class imbalance is not performed.

The notebook:
- Computes correlations on numeric features
- Visualizes correlation structure (e.g., heatmaps / automated visualization)
- Extracts **high-correlation feature pairs** (|corr| ≥ 0.80) to highlight likely multicollinearity
- Uses these results to recommend features that could be dropped to reduce redundancy

---
