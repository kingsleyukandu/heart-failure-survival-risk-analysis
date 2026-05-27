# Heart Failure Mortality Risk Analysis: From Statistical Analysis and Survival Modeling to Machine Learning Predictive Modeling

## Project Overview

This project analyzes a heart failure clinical records dataset to explore clinical factors associated with mortality outcomes among heart failure patients. The long-term goal is to build a complete health data analytics workflow that moves from data understanding and statistical analysis to survival analysis, Cox regression, and machine learning-based predictive modeling.

The project is currently in progress. At this stage, the completed work focuses on data inspection, exploratory data analysis, correlation analysis, and statistical testing. Machine learning models, survival analysis, and Cox regression have not yet been completed and are listed as future phases.

This README documents the work completed so far and will be updated as the project progresses.

---

## Current Project Status

| Phase | Status |
|---|---|
| Data loading and inspection | Completed |
| Missing value and duplicate checks | Completed |
| Exploratory data analysis | Completed |
| Correlation analysis | Completed |
| Statistical hypothesis testing | Completed |
| Survival analysis | Planned |
| Cox proportional hazards regression | Planned |
| Machine learning predictive modeling | Planned |
| Final model evaluation and reporting | Planned |

---

## Research Goal

The current goal is to understand which clinical variables show meaningful statistical differences between patients who experienced a death event and those who did not during the follow-up period.

The broader project goal is to answer the following question:

> Which clinical characteristics are associated with mortality outcomes among heart failure patients, and how can statistical analysis, survival analysis, and machine learning be combined to study patient risk responsibly?

At the current stage, the analysis focuses only on exploratory and statistical evidence. Predictive modeling results will be added in later phases.

---

## Dataset Summary

The dataset contains clinical records for heart failure patients.

| Item | Summary |
|---|---:|
| Number of patients | 299 |
| Number of variables | 13 |
| Missing values | 0 |
| Duplicate rows | 0 |
| Patients with `DEATH_EVENT = 0` | 203 |
| Patients with `DEATH_EVENT = 1` | 96 |
| Death event proportion | 32.1% |
| No observed death event proportion | 67.9% |

The target variable is `DEATH_EVENT`:

- `DEATH_EVENT = 1`: the patient experienced a death event during follow-up.
- `DEATH_EVENT = 0`: the death event was not observed during follow-up.

The `time` variable represents follow-up duration.

---

## Variables in the Dataset

| Variable | Description |
|---|---|
| `age` | Patient age |
| `anaemia` | Whether the patient had anaemia |
| `creatinine_phosphokinase` | Enzyme level related to muscle or tissue damage |
| `diabetes` | Whether the patient had diabetes |
| `ejection_fraction` | Percentage of blood pumped out of the heart during contraction |
| `high_blood_pressure` | Whether the patient had high blood pressure |
| `platelets` | Platelet count in the blood |
| `serum_creatinine` | Kidney-related blood marker |
| `serum_sodium` | Sodium level in the blood |
| `sex` | Patient sex |
| `smoking` | Smoking status |
| `time` | Follow-up duration |
| `DEATH_EVENT` | Mortality outcome indicator |

---

## Completed Work So Far

### 1. Data Loading and Inspection

The dataset was loaded and inspected to understand its structure, variable types, and overall quality.

Completed checks included:

- Previewing the dataset
- Checking the dataset shape
- Reviewing column names and data types
- Checking for missing values
- Checking for duplicate rows
- Generating descriptive statistics

Key observations:

- The dataset contains 299 patient records and 13 variables.
- No missing values were found.
- No duplicate rows were found.
- All variables are stored numerically, although several variables represent binary clinical categories.

---

### 2. Exploratory Data Analysis

Exploratory data analysis was performed to understand the distribution of clinical variables and how they differ across death event groups.

The analysis included:

- Target variable distribution
- Histograms for numerical variables
- Boxplots comparing numerical variables by `DEATH_EVENT`
- Cross-tabulations for categorical variables
- Assessment of skewness and possible outliers
- Visual comparison of patients with and without observed death events

#### Death Event Distribution

The outcome distribution shows moderate class imbalance:

| Death Event Status | Number of Patients | Percentage |
|---|---:|---:|
| `DEATH_EVENT = 0` | 203 | 67.9% |
| `DEATH_EVENT = 1` | 96 | 32.1% |

#### Numerical Feature Patterns

The exploratory analysis showed that several numerical variables were skewed or contained possible outliers.

Important patterns observed:

- `creatinine_phosphokinase` was strongly right-skewed and contained extreme values.
- `serum_creatinine` was right-skewed, with most values concentrated at lower levels.
- `serum_sodium` appeared approximately normal with some lower-end values.
- `platelets` appeared approximately normal with mild right skewness.
- Patients who experienced death events tended to be older.
- Patients who experienced death events tended to have lower ejection fraction.
- Patients who experienced death events tended to have higher serum creatinine.
- There was visible overlap between the two outcome groups, meaning no single variable perfectly separates patients by death event status.

#### Categorical Feature Patterns

Cross-tabulation was used to compare binary clinical indicators with `DEATH_EVENT`.

Observed patterns included:

- Patients with anaemia showed a higher death-event proportion than patients without anaemia.
- Patients with high blood pressure showed a higher death-event proportion than patients without high blood pressure.
- Diabetes, sex, and smoking showed smaller differences in death-event proportions in this dataset.

---

## Correlation Analysis

A correlation matrix was used to examine linear relationships among numerical variables and their association with `DEATH_EVENT`.

Variables with stronger observed correlation with `DEATH_EVENT` included:

| Variable | Correlation with `DEATH_EVENT` | Interpretation |
|---|---:|---|
| `serum_creatinine` | 0.29 | Higher values were associated with death events |
| `age` | 0.25 | Older age was associated with death events |
| `ejection_fraction` | -0.27 | Lower values were associated with death events |
| `serum_sodium` | -0.20 | Lower values were associated with death events |
| `time` | -0.53 | Shorter observed follow-up time was associated with death events |

The negative relationship between `time` and `DEATH_EVENT` reflects the survival structure of the dataset. Patients who experienced death events often had shorter observed follow-up durations.

Correlation does not imply causation. These results only describe observed relationships in this dataset.

---

## Statistical Analysis

Because several numerical variables were skewed and contained outliers, the Mann-Whitney U test was used instead of the independent samples t-test. The Mann-Whitney U test is a non-parametric test that compares whether values in one group tend to be higher or lower than values in another group without assuming normality.

The two groups compared were:

- Patients with `DEATH_EVENT = 1`
- Patients with `DEATH_EVENT = 0`

### Statistical Test Results

| Hypothesis | Variable Tested | Alternative Hypothesis | p-value | Result |
|---|---|---|---:|---|
| H1 | Age | Patients who experienced death events tend to be older | 8.34e-05 | Statistically significant |
| H2 | Serum creatinine | Patients who experienced death events tend to have higher serum creatinine | 7.90e-11 | Statistically significant |
| H3 | Serum sodium | Patients who experienced death events tend to have lower serum sodium | 0.000146 | Statistically significant |
| H4 | Ejection fraction | Patients who experienced death events tend to have lower ejection fraction | 3.68e-07 | Statistically significant |

---

## Key Findings So Far

The current statistical analysis suggests that several clinical variables differ significantly between patients who experienced death events and those who did not.

### 1. Age

Patients who experienced death events tended to be older than patients without observed death events. This suggests that age may be an important mortality-related factor in this dataset.

### 2. Serum Creatinine

Patients who experienced death events tended to have higher serum creatinine levels. Since serum creatinine is related to kidney function, this may suggest that kidney-related health status is associated with mortality outcomes in this dataset.

### 3. Serum Sodium

Patients who experienced death events tended to have lower serum sodium levels. This may indicate that sodium imbalance is associated with poorer outcomes in the dataset.

### 4. Ejection Fraction

Patients who experienced death events tended to have lower ejection fraction values. This aligns with the clinical expectation that weaker heart pumping function may be related to worse outcomes.

### 5. No Single Variable Fully Separates the Outcome Groups

Although several variables showed statistically significant differences, the visual analysis showed overlap between patients with and without observed death events. This supports the need for multivariable modeling in the next phases of the project.

---

## Next Phase: Machine Learning

The next phase of this project will focus on building machine learning models to predict `DEATH_EVENT` using patient-level clinical variables.

Planned models include:

- Logistic Regression
- Random Forest
- Gradient Boosting
- Support Vector Machine
- K-Nearest Neighbors

---

## Future Survival Analysis Work

A later phase of the project will use survival analysis methods to account for both event status and follow-up time.

Planned survival analysis methods include:

- Kaplan-Meier survival curves
- Log-rank tests
- Cox proportional hazards regression
- Hazard ratio interpretation
- Concordance index evaluation

This phase will help distinguish standard classification from time-to-event modeling.

---

## Disclaimer

This project is for educational, analytical, and portfolio-building purposes only. The analysis is not intended for clinical diagnosis, treatment planning, or replacement of professional medical judgment. Any real-world clinical application would require external validation, clinical review, ethical assessment, fairness evaluation, and regulatory consideration.

---