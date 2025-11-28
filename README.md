# Medicaid-Retinal-Detachment-Analysis

Predictive analysis of retinal detachment risk factors among Medicaid enrollees using administrative claims data (VEHSS Medicaid MAX, 2016–2019). Multivariable logistic regression examines independent contributions of age, diabetes, hypertension, and demographics to retinal detachment diagnosis, with comprehensive model validation and diagnostics.

---

## Predictors of Retinal Detachment Diagnosis in a Large Medicaid Population

Examining the contributions of age, diabetes, hypertension, and demographic factors using administrative claims data.

---

## Project Overview

This project analyzes the CDC's Vision and Eye Health Surveillance System (VEHSS) Medicaid Analytic eXtract (MAX) claims data to identify predictors of retinal detachment diagnosis among Medicaid enrollees. Using over 13.5 million original records from the Centers for Disease Control and Prevention (CDC), this analysis explores demographic and clinical risk factors, builds a multivariable logistic regression model, and provides rigorous model validation to support evidence-based public health surveillance.

---

## Objectives

- **Identify independent risk factors** for retinal detachment diagnosis among Medicaid enrollees, including age, sex, race/ethnicity, diabetes, hypertension, and major ocular conditions
- **Quantify the strength of association** between each predictor and retinal detachment using adjusted odds ratios with 95% confidence intervals
- **Validate model performance** using standard diagnostic methods (VIF, Hosmer–Lemeshow, ROC/AUC, calibration)
- **Provide actionable insights** for public health surveillance and clinical decision-making in vision health

---

## Research Question

**In Medicaid administrative claims data, what is the relative importance of age, diabetes, hypertension, and demographic characteristics in predicting retinal detachment diagnosis?**

---

## Dataset

| Attribute | Details |
|-----------|---------|
| **Source** | CDC Vision and Eye Health Surveillance System (VEHSS) Medicaid MAX |
| **Publisher** | Centers for Disease Control and Prevention |
| **Time Period** | 2016–2019 |
| **Original Records** | 13,593,123 rows × 37 columns |
| **Analytic Sample** | 651,317 records (after filtering for complete demographic data) |
| **Final Variables** | 14 columns |
| **Geographic Scope** | All 50 US states + Washington DC |
| **Data Type** | De-identified administrative claims (summary prevalence tables) |

**Data Source:** [Medicaid Claims (MAX) - Vision and Eye Health Surveillance](https://catalog.data.gov/dataset/medicaid-claims-max-vision-and-eye-health-surveillance)

**Downloaded Dataset:** [Medicaid_Claims__MAX__-_Vision_and_Eye_Health_Surveillance.csv](https://american0-my.sharepoint.com/:x:/g/personal/wn8924a_american_edu/IQCK8WQXqJlXQ6wc6Cve0q0iAcUlmCrXjtQb1nILo33GJNA?e=uwppnO)

---

## Methodology

### Study Design
Cross-sectional analysis of administrative claims data from 2016–2019.

### Participants
Medicaid enrollees with complete demographic and risk factor information (n = 651,317).

### Variables

**Outcome:**
- Binary indicator of retinal detachment diagnosis (yes/no)

**Predictors:**
- **Age group** (5 levels: 0–17, 18–39, 40–64, 65–84, 85+ years)
- **Sex** (Male, Female)
- **Race/Ethnicity** (Asian, Black non-Hispanic, Hispanic any race, North American Native, White non-Hispanic, Other, Unknown)
- **Diabetes** (binary: yes/no)
- **Hypertension** (binary: yes/no)
- **Major ocular condition** (binary: yes/no; includes glaucoma, cataract, diabetic retinopathy, AMD, retinal vein occlusion)

### Statistical Analysis

**1. Descriptive Statistics**
- Frequency distributions of all categorical variables
- Overall and stratified prevalence estimates
- Visual exploration of trends by age and demographic groups

**2. Multivariable Logistic Regression**
- Outcome: retinal detachment (binary)
- Model: `Retinal_Detachment ~ Age + Sex + RaceEthnicity + has_diabetes + has_hypertension + has_major_ocular_condition`
- Results: Adjusted odds ratios (ORs) with 95% confidence intervals

**3. Model Validation & Diagnostics**
- **Multicollinearity:** Variance Inflation Factors (VIF); all values < 5 acceptable
- **Goodness-of-fit:** Hosmer–Lemeshow test; non-significant p > 0.05 preferred
- **Discrimination:** ROC curve and Area Under the Curve (AUC)
- **Calibration:** Predicted vs. observed prevalence by decile

**4. Software & Packages**
- Language: R 4.0+
- Key packages: dplyr, ggplot2, summarytools, car (VIF), pROC (ROC/AUC), ResourceSelection (Hosmer–Lemeshow)

---

## Key Findings

### Overall Prevalence
- **Total analytic records:** 651,317
- **Overall prevalence of retinal detachment:** < 1%

### Prevalence by Age Group

The prevalence of retinal detachment varies by age group, with specific patterns emerging across the lifespan.

![Prevalence of Retinal Detachment by Age Group](https://github.com/weston-nyabeze/Medicaid-Retinal-Detachment-Analysis/blob/main/prevalence_by_age.png)

**Interpretation:** The bar chart displays retinal detachment prevalence across five age categories, allowing visual comparison of risk distribution in the Medicaid population.

---

### Multivariable Logistic Regression Results

After adjusting for all predictors, the following associations were observed:

**Forest Plot – Adjusted Odds Ratios:**

![Forest Plot: Adjusted Odds Ratios for Retinal Detachment](https://github.com/weston-nyabeze/Medicaid-Retinal-Detachment-Analysis/blob/main/forest_plot_odds_ratios.png)

**Interpretation:** 
- Points to the right of the vertical dashed line (OR = 1) indicate increased odds of retinal detachment.
- Points to the left indicate decreased odds.
- Error bars (95% CI) crossing the reference line indicate non-significant associations (p > 0.05).
- Blue points indicate statistically significant predictors; gray points indicate non-significant predictors.

---

## Model Performance

### Discrimination Ability (ROC Curve & AUC)

The model's ability to discriminate between cases with and without retinal detachment was evaluated using the ROC curve and AUC.

![ROC Curve: Retinal Detachment Prediction Model](https://github.com/weston-nyabeze/Medicaid-Retinal-Detachment-Analysis/blob/main/roc_curve.png)

| Metric | Value |
|--------|-------|
| **AUC** | 0.6002 |
| **95% CI** | [0.5928, 0.6076] |
| **Interpretation** | Modest discrimination; model performs better than chance but has limited predictive power for this rare outcome |

---

### Model Diagnostics Summary

| Diagnostic Test | Result | Interpretation |
|-----------------|--------|----------------|
| **Multicollinearity (VIF)** | All values < 5 | No problematic multicollinearity |
| **Hosmer–Lemeshow Test** | p > 0.05 | Adequate model fit |
| **Calibration** | See calibration plot | Agreement between predicted and observed values |

---

## Limitations

1. **Administrative Claims Data:**
   - Relies on diagnostic coding accuracy; potential for misclassification
   - Limited clinical detail (e.g., severity, laterality, symptom onset)
   - Reflects diagnosed cases only; undiagnosed retinal detachment not captured

2. **Study Population:**
   - Limited to Medicaid enrollees; findings may not generalize to privately insured or uninsured populations
   - Temporal scope: 2016–2019 snapshot; trends over time unknown

3. **Model Performance:**
   - AUC of 0.60 indicates modest discrimination, typical for rare outcomes in administrative data
   - Unmeasured confounding from variables not available in claims data

4. **Missing Data:**
   - Records excluded due to incomplete demographic or risk factor data; potential selection bias

---

## Author

**Weston Nyabeze**

- 🎓 Education: American University
- 💼 Specialization: Healthcare Analytics
- 🔗 LinkedIn: [www.linkedin.com/in/weston-nyabeze](https://www.linkedin.com/in/weston-nyabeze)

---
## License

This project is licensed under the **MIT License**. See the [`LICENSE`](LICENSE) file for details.

---
## Acknowledgments

### Academic Institution
- **American University** – Educational support and institutional affiliation

### Data Sources
- **Centers for Disease Control and Prevention (CDC)** – Vision and Eye Health Surveillance System (VEHSS)
- **Medicaid Analytic eXtract (MAX) Program** – Administrative claims data access and documentation
- **Data.gov** – [Medicaid Claims (MAX) - Vision and Eye Health Surveillance](https://catalog.data.gov/dataset/medicaid-claims-max-vision-and-eye-health-surveillance)

### Tools & Assistance
- **Perplexity AI** – Research assistance, code optimization, and analytical guidance
- **R Ecosystem** – dplyr, ggplot2, pROC, car, and ResourceSelection packages

---


