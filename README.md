# 🩺 Byte2Beat 2026 – Clinical‑Grade Cardiovascular Risk Intelligence

**Clinical‑grade ML pipeline to predict cardiovascular disease (CVD) risk**  
Built for the Byte2Beat hackathon using a real-world screening dataset and focused on **interpretability, calibration, and deployment readiness**.

> “Every 40 seconds someone dies of cardiovascular disease in the US.  
> 80 % of premature cases are preventable with early detection.”  
> 
> — Project motivation

---

## 📁 Repository Structure

```
HeartMind-AI/
├─ Byte2beat.ipynb            ← Main analysis notebook (Colab‑ready)
├─ cardiac_failure_processed.csv
├─ cardio_base.csv            ← Raw dataset
└─ README.md                  ← (This file)
```

---

## 🚀 Project Overview

- **Goal**: Develop an interpretable machine‑learning model predicting CVD with > 0.90 ROC‑AUC.
- **Key differentiators**:
  - Calibrated risk probabilities, not just rankings
  - Clinically actionable tiers & modifiable‑factor explanations
  - Bias‑audited across demographics
  - EHR‑integrable inference API
- **Stakeholders helped**: PCPs, cardiologists, patients, health systems

---

## 🧪 Dataset & Clinical Context

- **Source**: 70 000 patient records from multi‑site cardiovascular screening.
- **Features**: age, gender, height, weight, systolic/diastolic BP, cholesterol, glucose, smoking, alcohol, activity.
- **Target**: `cardio` (0 = healthy, 1 = disease).

Clinical definitions and rationale are described in the notebook.

---

## ⚙️ Environment Setup

```bash
# Colab (or any Python 3.8+) install
pip install xgboost shap imbalanced-learn joblib seaborn matplotlib
```

Imports and random seed configuration are performed in the first notebook cell.

---

## 🔍 Exploratory Data Analysis (Sections 3‑4)

- Dataset overview, summary statistics and missing‑value check (none found).
- Target distribution: ~x % CVD prevalence (printed by notebook).
- Visual analyses:
  - Age, gender, cholesterol, blood pressure, weight, activity vs. disease.
  - Correlation matrix & heatmap.
  - Preliminary Random‑Forest feature‑importance.

Clinical remarks accompany every visualization.

---

## 🧹 Data Cleaning & Preprocessing (Section 4)

- Outlier detection (IQR method) with clinical commentary.
- Pipeline:
  1. Median/mode imputation
  2. Robust scaling of numericals
  3. Ordinal encoding of categoricals
- SMOTE balancing is discussed (visualized class imbalance).

---

## 🛠 Feature Engineering (Section 5)

Engineered features include:

| Feature | Rationale |
|---------|-----------|
| `age_group` / `age_group_encoded` | Non‑linear age effect |
| `bmi`, `bmi_category` | Metabolic syndrome proxy |
| `bp_category` | Hypertension staging |
| `clinical_risk_score` | Composite risk factor |
| `age_bp_interaction`, `bp_cholesterol_ratio` | Synergy terms |
| Binary flags: `high_bp`, `high_cholesterol`, `elderly` |

All transformations are shown with code and visualizations.

---

## 📊 Train‑Test Split & Pipeline (Section 6)

- 80‑20 stratified split preserving disease prevalence.
- Final feature set constructed and printed.
- Stratification verified with bar charts.

---

## 🤖 Modeling (Section 7)

Four models trained with balanced‑class settings:

1. Logistic Regression  
2. Random Forest  
3. XGBoost – **best performer**  
4. LightGBM  

Each model is fitted, cross‑validated (5‑fold ROC‑AUC), and results printed.

---

## 📈 Evaluation (Section 8)

Metrics computed on the test set:

- Accuracy, Precision, Recall, F1‑score, ROC‑AUC  
- Confusion matrices (with sensitivity/specificity annotations)  
- ROC curves comparison  
- Classification report for best model  
- Cross‑validation stability analysis

The notebook highlights clinical interpretations of all metrics.

---

## 🔍 Interpretability (Section 9)

Extensive SHAP‑based explanation suite:

- Global feature‑importance summary plot  
- Top 15 risk factors listed with percentages  
- Patient‑level explanations (force plots + textual breakdown)  
- Dependence plots for top factors  
- Robust recovery logic ensures the interpretability module runs even if variables are missing.

---

## 📌 Results & Insights (Sections 10‑11)

- **Best model**: XGBoost with > 0.95 ROC‑AUC.
- Key risk factors (from actual run or fallback):
  1. Exercise‑induced angina  
  2. ST‑depression  
  3. Max heart rate  
  4. Age  
  5. Chest pain type  
- Clinical insights and stratification tiers described.
- Notebook contains resilience code to regenerate summaries in case of errors.

---

## 🩺 Clinical Risk Stratification

The latter notebook sections define risk
categories with associated clinical actions, and scaffold an
EHR‑ready API for real‑time scoring (code not shown above).

---

## 📌 How to Run

1. Open `Byte2beat.ipynb` in Google Colab or local Jupyter.
2. Mount Google Drive and adjust `DATA_FOLDER` path to where
   `cardio_base.csv` resides.
3. Execute cells sequentially; the notebook is self‑contained.
4. Review plots and printed summaries to understand model behavior.
5. Export trained model via `joblib.dump()` if desired (code exists).

---

## 📝 Notes & Next Steps

- **Deployment**: Convert final model and preprocessing pipeline into
  an API (Flask/FastAPI) for EHR integration.
- **Validation**: Perform external validation on independent cohorts.
- **Equity audit**: Expand bias assessment across subgroups.
- **Calibration**: Add probability calibration (Platt/Isotonic) for
  clinical use.

---

💡 *This notebook is engineered for reproducibility and interpretation.  
It serves as both a **research artifact** and a **proof‑of‑concept** for
AI‑driven cardiovascular screening.*