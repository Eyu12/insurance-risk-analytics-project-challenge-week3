

# 📊 Task 1 – Data Import & Exploratory Data Analysis (EDA)

AlphaCare Insurance Solutions (ACIS) is analyzing historical insurance data to identify risk patterns, understand customer behavior, and prepare the dataset for predictive modeling.
Task 1 focuses on loading, cleaning, and exploring the dataset.

## 🎯 Objective of Task 1

Load the raw insurance dataset from a pipe-delimited .txt file.
Clean missing, blank, and inconsistent values.
Create important variables such as Loss Ratio.
Perform exploratory data analysis (EDA).
Visualize major patterns affecting risk and claims.

## 📁 1. Data Loading
- The raw data is stored in insurance_data.txt and is pipe-delimited (|).
- low_memory=False ensures correct data type handling during import.

## 🧹 2. Data Cleaning
- Replace blank and space-only values
- Convert date column
- Create Loss Ratio

## 🔍 3. Exploratory Data Analysis (EDA)
- Dataset overview
- Key insights include:
  - Missing data is concentrated in fields like Citizenship, Occupation, and CustomerCategory.
  - Numerical fields show heavy skewness, especially claims and premiums.
  - TransactionMonth column has consistent and valid date values.

## 📈 4. Visual Insights
- Loss Ratio by Province
- Distribution of Total Claims
- Relationship Between Premium and Claims
These visualizations highlight regional risk levels, claim frequency patterns, and relationships between key financial metrics.

## 📝 5. Summary of Task 1
- The dataset loads successfully using a pipe (|) separator.
- Missing and blank values have been cleaned.
- LossRatio was engineered as a key analytical metric.
- Initial EDA exposes differences in risk by province and customer type.
- Plots reveal strong claim–premium relationships and skewed financial features.

# Task 2: Reproducible and Auditable Data Pipeline with DVC

## Overview
In finance and insurance, it is crucial to have **reproducible and auditable analyses** for regulatory compliance, debugging, or auditing. Task-2 demonstrates how to use **Data Version Control (DVC)** to track datasets and ensure any analysis or model can be reproduced.

DVC allows you to version your datasets, track changes, and store data in a remote location, while Git tracks the `.dvc` metafiles.


## Steps Completed

### 1. Branch Setup
- Created a new branch `task-2` for this task.
- Merged necessary changes from Task-1 into `main` prior to starting Task-2.

### 2. DVC Installation
- pip install dvc

### 3. Initialize DVC
- Initializes DVC in the project folder.
- Creates .dvc directory and configuration files.

### 4. Configure DVC Remote Storage
- Created a dedicated folder for DVC storage:
- Added the folder as the default DVC remote:
- dvc remote add -d localstorage 

### 5. Add Dataset to DVC
- Dataset used: data/processed/cleaned_insurance_data.csv
- dvc add "data/processed/cleaned_insurance_data.csv"
- This generates a .dvc file  that tracks the dataset version.

### 6. Commit Changes to Git
- .dvc file is now tracked by Git while the actual dataset remains ignored.

### 7. Push Data to DVC Remote
- Copies the dataset to the configured DVC remote (insurance-dvc-storage).
- Ensures reproducibility and auditable data versions.

## Key Notes
- .dvc files track the metadata of datasets and are tracked in Git.
- Raw datasets can be ignored by Git to avoid large repository sizes.
- DVC ensures you can reproduce analysis with the exact same data version.
- dvc status can be used to check if tracked data is up-to-date.
