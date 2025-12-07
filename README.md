
# 📘 End-to-End Insurance Risk Analytics & Predictive Modeling

## Objective:
Analyze historical car insurance data for AlphaCare Insurance Solutions (ACIS) to identify low-risk customers, optimize premiums, and improve marketing targeting.

## 🎯 Business Goals
- Find low-risk customer segments
- Understand what drives claims and losses
- Build predictive models for claim severity and probability
- Use data to set risk-based premiums
- Make actionable business recommendations

## Project Structure 
bash 
 .
├── .dvc/                  # DVC configuration for data versioning
├── .github/               # GitHub workflows
├── .venv/                 # Virtual environment
├── data/
│   ├── processed/         # Processed datasets
│   ├── raw/               # Raw datasets
├── dvc_data/
│   ├── cleaned_insurance_data.csv
│   └── cleaned_insurance_data.csv.dvc
├── notebooks/
│   ├── models/            # Model scripts and experiments
│   ├── plots/             # Plots and visualizations
│   ├── reports/           # Report notebooks
│   ├── task1_eda.ipynb
│   ├── task3_ab_hypothesis_testing.ipynb
│   └── task4_modeling.ipynb
├── reports/               # Generated reports
├── README.md
└── requirements.txt       # Python dependencies



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

# 🧪 Task 3 — Statistical Validation of Key Risk Drivers

This task focuses on statistically validating or rejecting key hypotheses related to **risk** and **margin** variations across customer and geographic attributes. These findings support the development of a more effective segmentation strategy.

---

## 🎯 Objective

Determine whether specific features (Province, Zip Code, Gender) significantly affect:

- **Claim Frequency** – % of policies with ≥1 claim  
- **Claim Severity** – Average claim amount (for claimers only)  
- **Margin** – TotalPremium − TotalClaims  

The goal is to identify statistically meaningful segmentation variables.

---

## 📊 Null Hypotheses Tested

| Hypothesis | Description |
|-----------|-------------|
| **H₀₁** | No risk differences across provinces |
| **H₀₂** | No risk differences between zip codes |
| **H₀₃** | No significant margin difference between zip codes |
| **H₀₄** | No significant risk difference between Women and Men |

---

## 🛠️ Methodology

### **1. Select Metrics**
- Claim Frequency  
- Claim Severity  
- Margin  

### **2. Data Segmentation**
Split the data into:

- **Group A (Control Group)**  
- **Group B (Test Group)**  

For multi-class features (e.g., provinces), two categories may be selected to form A/B groups.  
These groups must be equivalent on unrelated variables.

---

### **3. Statistical Tests Applied**

| Scenario | Test |
|----------|------|
| Categorical vs Categorical | Chi-Squared Test |
| Numeric vs Categorical (two groups) | Independent t-test / Z-test |
| Numeric vs Categorical (multiple groups) | ANOVA |

---

### **4. Decision Rule**

- Reject H₀ if **p-value < 0.05** → Feature impacts risk/margin  
- Fail to reject H₀ if **p ≥ 0.05** → No significant impact  

---

## 📝 Deliverables

- Clear KPIs  
- Segmentation criteria  
- Statistical test results  
- p-value summary table  
- Final interpretation for each hypothesis  
- Business recommendations for rejected hypotheses  

### Example Interpretation:
> We reject H₀ for provinces (p < 0.01). Gauteng shows 15% higher loss ratios than Western Cape. Regional premium adjustments are recommended.

---

## 🔧 Git Requirements

- Merge Task-2 PR into main  
- Create branch **task-3**  
- Commit changes with meaningful messages  
- Submit PR for review  

---

## 📦 Output

- `task_3_hypothesis_testing.ipynb`  
- `task_3_results.csv`  
- `task_3_report.md`  

---

# 🤖 Task 4 — Predictive Modeling for Risk-Based Pricing

Task 4 focuses on building machine learning models to support a **dynamic, risk-based pricing system**.  
This includes both regression modeling (claim severity) and classification modeling (claim probability).

---

## 🎯 Goals

### **1. Claim Severity Prediction (Regression)**
Predict `TotalClaims` for records where claims > 0.

Metrics:  
- RMSE  
- R²  

### **2. Premium Optimization Model**
Predict the most appropriate premium using ML models.

### **Advanced (Recommended):**  
Predict claim probability using a classification model:


---

## 🛠️ Workflow

### **1. Data Preparation**
- Handle missing values  
- Perform feature engineering  
- Encode categorical data (One-Hot, Label Encoding)  
- Train-test split (70:30 or 80:20)

---

### **2. Models Implemented**

#### Regression
- Linear Regression  
- Random Forest Regressor  
- Gradient Boosting / XGBoost  

#### Classification (Optional but recommended)
- Logistic Regression  
- Random Forest Classifier  
- XGBoost Classifier  

---

### **3. Model Evaluation**

#### Regression Metrics:
- RMSE  
- MAE  
- R²  

#### Classification Metrics:
- Accuracy  
- Precision  
- Recall  
- F1-score  
- ROC-AUC  

A comparison table should be included in the report.

---

## 🔍 Model Interpretability

Use:

- **SHAP**  
- **LIME**

Extract **Top 5–10 most influential features** and provide business interpretation.

### Example Insight:
> SHAP shows vehicle age strongly increases predicted claim severity. Premium rates should account for higher risk in older vehicles.

---

## 📝 Deliverables

- Clean data preparation script  
- Modeling scripts (regression & classification)  
- Evaluation metrics summary  
- SHAP/LIME plots  
- Final business recommendations  

---

## 🔧 Git Requirements

- Merge Task-3 branch into main  
- Create **task-4** branch  
- Commit frequently with descriptive messages  
- Submit PR after completing the task  

---

## 📦 Output

- `task_4_modeling.ipynb`  
- `model_performance_summary.csv`  
- `shap_analysis/` folder  
- `task_4_report.md`  

---

