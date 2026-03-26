# Heart Disease Analysis & Machine Learning

## Overview

This project explores a real-world biomedical dataset to analyze factors associated with cardiovascular disease and develop predictive machine learning models.

Using the **UCI Heart Disease dataset**, the project includes a complete workflow covering:

- data cleaning and preprocessing
- exploratory data analysis (EDA)
- statistical inference
- machine learning modeling
- interactive visualization with Shiny

## Objectives

The main goals of this project were:

- identify relationships between clinical variables and heart disease
- compare characteristics between healthy and diseased patients
- assess statistical associations between variables
- build predictive models to classify disease presence
- evaluate model performance using standard metrics

## Dataset

- **Source:** UCI Heart Disease Data
- **Accessed from:** Kaggle
- **Original size:** 920 observations, 16 variables

The dataset includes clinical and demographic variables such as:

- age
- sex
- chest pain type
- resting blood pressure
- cholesterol
- fasting blood sugar
- resting ECG
- maximum heart rate achieved
- exercise-induced angina
- ST depression
- ST slope
- disease diagnosis

## Data Preprocessing

The following preprocessing steps were applied:

- imported the dataset in R
- converted empty values to `NA`
- examined missing values
- removed variables with excessive missingness:
  - `ca` (66.4% missing)
  - `thal` (52.8% missing)
- removed incomplete observations using `complete.cases()`
- converted categorical and logical variables to factors
- renamed the original target variable `num` to `diagnosis`
- created:
  - `diagnosis` as an **ordinal factor** with 5 levels (`0` to `4`)
  - `diagnosis_bin` as a **binary factor**:
    - `0` = no heart disease
    - `1` = heart disease

### Final dataset

- **531 observations**
- **15 variables**

## Exploratory Data Analysis

The descriptive analysis showed that patients with heart disease tend to:

- be slightly older
- have higher resting blood pressure
- present lower maximum heart rate (`thalch`)
- show higher ST depression (`oldpeak`)

### Main exploratory findings

- **Chest pain type (`cp`)** is strongly associated with disease presence
- **Exercise-induced angina (`exang`)** shows a clear association with disease
- **ST slope (`slope`)** also differs notably between healthy and diseased patients
- **Fasting blood sugar (`fbs`)** showed only a weak association with disease in this sample

Both numerical and categorical variables were explored using:

- summary statistics
- frequency tables
- boxplots
- histograms
- grouped barplots
- pairwise correlation plots

## Statistical Analysis

### Risk analysis

A custom R function was defined to calculate:

- exposed risk
- non-exposed risk
- risk difference
- relative risk (RR)
- odds ratio (OR)

Example results:

- **Male vs Female**
  - Relative Risk = 2.23
  - Odds Ratio = 5.15

- **Exercise-induced angina**
  - Relative Risk = 2.14
  - Odds Ratio = 7.84

These results suggest strong associations for some clinical variables.

### Probability analysis

Several probability-based questions were explored, including:

- probability of heart disease in the study population
- probability of disease by sex
- probability of disease by chest pain type
- conditional probability of disease given exercise-induced angina

### Chi-square test

A chi-square test was used to assess the relationship between fasting blood sugar (`fbs`) and heart disease.

- **p-value = 0.3777**

This suggests no statistically significant association in this dataset.

### Simulation

A simple simulation was performed using a binomial model to estimate how many individuals out of 10,000 would be expected to have cardiovascular disease based on the observed prevalence.

## Machine Learning

Because the dataset contains labeled outcomes, a **supervised learning** approach was selected.

### Support Vector Machine (SVM)

SVM models were trained using two target variables:

1. **Binary target:** `diagnosis_bin` (`0` / `1`)
2. **Multiclass target:** `diagnosis` (`0` / `1` / `2` / `3` / `4`)

Two kernels were compared:

- linear kernel (`vanilladot`)
- radial basis function kernel (`rbfdot`)

### Results

#### Binary classification (`diagnosis_bin`)

| Kernel | Accuracy | Sensitivity | Specificity |
|--------|----------|-------------|-------------|
| Linear | 0.8302 | 0.9072 | 0.7097 |
| RBF | 0.7987 | 0.9072 | 0.6290 |

The **linear SVM** achieved the best performance for binary classification.

#### Multiclass classification (`diagnosis`)

| Kernel | Accuracy |
|--------|----------|
| Linear | 0.5380 |
| RBF | 0.5443 |

Performance was lower for multiclass classification, likely due to:

- increased class complexity
- fewer observations in higher disease severity levels

## Multiple Linear Regression

A multiple linear regression model was fitted using **maximum heart rate (`thalch`)** as the dependent variable.

### Significant predictors included:

- age
- chest pain type
- cholesterol
- resting ECG
- exercise-induced angina
- ST slope

### Model performance

- **R-squared = 0.4123**
- **Adjusted R-squared = 0.3964**
- overall model p-value `< 2.2e-16`

This indicates moderate explanatory power.

A stepwise model selection procedure (`step()`) was also applied to identify the most informative predictors.

## ANOVA

An ANOVA was performed to determine whether **maximum heart rate (`thalch`)** differed significantly across the five diagnosis groups.

### Result

- **p-value < 2e-16**

This indicates statistically significant differences in `thalch` between diagnosis groups.

### Tukey post-hoc test

The main significant differences were found between:

- the healthy group (`0`)
- and all disease groups (`1`, `2`, `3`, `4`)

## Shiny App

A Shiny app was developed as an interactive data visualization tool.

### Features

- upload a dataset (`.csv`, `.tsv`, `.txt`)
- choose separators and decimal format
- remove rows with missing values
- convert character and logical variables to factors
- select numerical and categorical variables
- view:
  - data preview
  - summary statistics
  - boxplots

This app provides a simple interface for quick exploration of biomedical datasets.

## Main Findings

- heart disease was associated with older age and lower maximum heart rate
- binary classification performed much better than multiclass prediction
- the linear SVM was the best-performing classification model in this study
- maximum heart rate differed significantly across diagnosis groups

## Limitations

This dataset has several important limitations:

- high percentage of missing values in some variables
- removal of `ca` and `thal` reduced the number of available predictors
- complete-case analysis reduced the sample size from 920 to 531
- the sample is heavily male-dominated, which may affect generalizability
- the dataset lacks relevant lifestyle variables such as:
  - smoking
  - alcohol consumption
  - BMI
  - body weight
- multiclass prediction is affected by class imbalance

## Tech Stack

- **R**
- **R Markdown**
- **Shiny**

### R packages

- `Hmisc`
- `dplyr`
- `knitr`
- `caTools`
- `kernlab`
- `caret`
- `nortest`
- `shiny`
- `shinythemes`
- `DT`
