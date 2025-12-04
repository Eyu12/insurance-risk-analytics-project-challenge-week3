

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