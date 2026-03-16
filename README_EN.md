# **Statistical Analysis of the CBM Project (HGF_UVALPO)**

This repository contains the detailed statistical analysis of the **CBM Project (Childbirth Experience Questionnaire / BMSP2)** conducted for the Hospital Dr. Gustavo Fricke (HGF) and the University of Valparaíso (UVALPO).

The primary objective of this document and the accompanying code is to ensure methodological **transparency, rigor, and reproducibility** in accordance with the standards required by reviewers and editors of journals indexed in the Web of Science (WOS) or other high-impact scientific databases.

---

## 📌 **Overview**

The assessment of quality of care and childbirth experience in women was examined using the BMSP2 tool. To guarantee the validity of the inferential analysis, robust parametric statistical models were employed, adjusting for relevant demographic covariates and mitigating the impact of potential biases in the observational data.

## 📂 **Dataset and Ethical Considerations**

- The analyzed data comes from an anonymized dataset, thus respecting the confidentiality of the participants.
- The dataset has been preprocessed to protect anonymity, complying with the guidelines of the Declaration of Helsinki (`datos_encuestas.csv` obtained from a private repository). No sensitive data allowing direct identification of the patients is exposed.

---

## 📊 **Methodology and Analysis Structure**

The iterative source code within the Jupyter Notebook (`Statistical Analysis of the CBM Project (HGF_UVALPO) IJGO.ipynb`) exhaustively documents each phase of the data flow, broken down into the following stages:

### 1. **Data Cleaning and Preprocessing**

- **Standardization:** Normalization of numerical formats in scalar items and controlled imputation of values (NaN = 0 / neutral as logically corresponded) to ensure compatibility with statistical methods.
- **Reverse Scoring:** Coded processing of BMSP2 control items whose wording implies a reverse construct (e.g., questions with negative polarity), parametrically mapping values according to the instrument's specifications.

### 2. **Descriptive Analysis**

- Univariate statistics of the cohort (mean, median, standard deviation).
- Demographic distributions focusing on **Age, Educational Level, and Parity**.
- Frequency tabulations for response counts (5-point scale) item by item.

### 3. **Calculation of Dimensions (BMSP2 Instrument)**

Individual items were statistically grouped into the corresponding seven previously validated theoretical dimensions:

1. *Relational quality care*
2. *Depersonalized care*
3. *Continuous family participation*
4. *Timely and respectful care*
5. *Comfortable physical environment*
6. *Conditions of mother-child contact*
7. *Self-care and comfort*

### 4. **Bivariate Inferential Analysis**

Inferential tests were executed followed by post-hoc comparisons (such as the Kruskal-Wallis or Mann-Whitney U test and Dunn's test) if the assumption of normal variances was rejected, analyzing the dimensions by:

- **Type of Delivery** (Vaginal vs. Cesarean). *Methodological Note:* Forceps-assisted delivery was intentionally excluded from the main model due to low sample frequency (Outliers) introducing excessive variance (lack of statistical power).
- **Parity** (Nulliparous vs. Multiparous).
- **Educational Level** and grouping by **Age**.

### 5. **Multivariate Analysis: Robust Linear Regression (RLM)**

Designed to control for heteroscedasticity and the possible presence of clinical outliers, a **Robust Linear Regression** was formulated using Huber's norm (Huber's T-norm or M-estimator).

- **Main Model:** The primary effect of interest analyzed was the *Impact of the Type of Delivery (Cesarean vs. Vaginal)* on each clinical dimension, **simultaneously adjusting** the model for critical explanatory covariates (`Age`, `Educational_level`, and `Parity`).
- **Verification of Assumptions:** Rigorous exploratory visualization of residuals vs. fitted values, guaranteeing statistical independence, homoscedasticity, and linearity.

---

## 🛠️ **Requirements and Reproducibility**

The pipeline was written and tested in a **Python 3** environment. The analysis relies extensively on the architecture of the `statsmodels` library (Robust Linear Regressions RLM) and `pingouin` for cross-validation tests.

To reproduce this analysis locally in a Jupyter Notebook instance or in Google Colab, the following dependencies are required (libraries listed according to the block #0 imports):

```python
pandas
numpy
matplotlib
seaborn
scipy
statsmodels
scikit-posthocs
pingouin
```

*(You can install them quickly within the environment by running: `pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-posthocs pingouin -q`)*

### Execution

Open the `.ipynb` notebook and execute all cells sequentially in a Python kernel. The notebook includes intrastructural comments and will connect with the Dataframe hosting the CSV, instantiating the statistical models in an automated way over the session.
