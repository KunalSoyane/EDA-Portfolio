# EDA Portfolio — Kunal Vivek Soyane

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/KunalSoyane/EDA-Portfolio/blob/main/EDA_Portfolio.ipynb)

Structured exploratory data analysis across three domains — health, financial, and retail — built around a reusable `EDAAnalyser` pipeline class.

---

## Datasets

| # | Domain | Dataset | Rows | Features | Target |
|---|--------|---------|------|----------|--------|
| 1 | Health | Pima Indians Diabetes (UCI) | 768 | 8 | Outcome (diabetes) |
| 2 | Financial | Loan Application Records (synthetic) | 1,000 | 7 | loan_approved |
| 3 | Retail | Transaction Records (synthetic) | 900 | 6 | return_flag |

---

## Pipeline

Every dataset runs through the same `EDAAnalyser` class in sequence:

```
1. Overview          →  dtypes, null counts, descriptive statistics
2. Missing Report    →  null percentage per column + pattern heatmap
3. Imputation        →  median fill (configurable: mean / mode)
4. Outlier — IQR     →  fence boundaries, count, % flagged + boxplots
5. Outlier — Z-score →  flags at |z| > 3.0
6. Distributions     →  histogram + KDE overlay per feature
7. Skewness Report   →  interpreted: symmetric / moderate / high skew
8. Correlation       →  lower-triangle Pearson heatmap, |r| > 0.75 flagged
9. VIF Analysis      →  multicollinearity detection (threshold: VIF > 10)
10. Pair Plot        →  selected features, coloured by target
```

---

## Key Observations

**Health — Pima Diabetes**
- Glucose, Insulin, BMI, SkinThickness, and BloodPressure contain zero values that are physiologically impossible — treated as missing and imputed with median
- Insulin has the highest missing rate (~49%) and strong right skew
- Glucose is the strongest single predictor of the target

**Financial — Loan Applications**
- Income and loan_amount follow log-normal distributions (high right skew)
- debt_to_income has moderate VIF — correlated with income and loan_amount as expected
- credit_score is the dominant separation factor between approved and rejected applications

**Retail — Transactions**
- Revenue is algebraically derived (price × quantity × (1 − discount)) — excluded from VIF to prevent artificial inflation
- 15 outlier transactions were injected to simulate bulk/wholesale orders — correctly detected by both IQR and Z-score methods
- Return rate increases with transaction value (expected: higher-value items returned more)

---

## Stack

```
Python · pandas · NumPy · matplotlib · seaborn · scipy · statsmodels
```

---

## Run Locally

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels
jupyter notebook EDA_Portfolio.ipynb
```

Or open directly in Colab with the badge above — no setup required.

---

## Author

**Kunal Vivek Soyane**  
[GitHub](https://github.com/KunalSoyane) · [LinkedIn](https://linkedin.com/in/kunal-vivek-soyane)
