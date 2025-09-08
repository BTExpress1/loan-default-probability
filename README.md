## 📓 Project Notebooks

# 💳 Loan Default Probability Prediction  

![Python](https://img.shields.io/badge/python-3.11-blue)  
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.3+-F7931E?logo=scikit-learn&logoColor=white)  
![LightGBM](https://img.shields.io/badge/LightGBM-3.3+-00599C)  
![SHAP](https://img.shields.io/badge/SHAP-0.44+-red)  
![JupyterLab](https://img.shields.io/badge/JupyterLab-4.0+-F37626?logo=Jupyter&logoColor=white)  

---

## 📌 Project Overview

This project predicts the **probability of loan default** using the LendingClub dataset (Kaggle).  

The goal is not just binary default prediction but **calibrated probability scoring** to enable **risk-based decision making** for lenders.  

- **Dataset:** LendingClub loan dataset (>2 GB, 50+ features retained after wrangling)  
- **Modeling Approach:** Logistic Regression, XGBoost, and LightGBM were benchmarked.  
- **Final Model:** Tuned & calibrated **LightGBM** selected for deployment.  
- **Key Outcome:** Default probabilities that allow risk teams to set **recall-focused or balanced thresholds**.  

---

## ⚠️ Memory Warning

The raw LendingClub dataset is **large (>2.4 GB compressed, ~6 GB in-memory)**.  

- Always work with the **sample (`loan_default_slim55.parquet`)** during exploration.  
- The **full dataset (`loan_default_full55.parquet`)** has already been reduced to the same 54 features and saved for you.  
- **Do not flip `USE_SAMPLE=False` inside Notebook 1** — this will attempt to load the raw CSV and crash most local machines.  
Instead, rely on the pre-saved parquet files.

---

## 🛠 Project Structure

├── data/
│ ├── processed/
│ │ ├── loan_default_slim55.parquet # sample dataset (~10% rows)
│ │ ├── loan_default_full51.parquet # full dataset, reduced features
│ │ ├── columns_to_keep.txt # final 54 feature names
│
├── notebooks/
│ ├── 1_data_wrangling_EDA.ipynb # Cleaning + exploratory analysis
│ ├── 2_preprocessing_training.ipynb # Preprocessing + baseline models
│ ├── 3_modeling_results.ipynb # Tuning, SHAP, KS, final outputs
│
├── models/
│ ├── preprocessor_final.joblib # Preprocessing pipeline
│ ├── lgbm_model_calibrated.joblib # Final calibrated LightGBM model
│ ├── metadata_final.json # Metadata (metrics, thresholds, timestamp)
│ ├── default_risk_report.csv # Top 10 borrowers with SHAP drivers
│
├── README.md # Project documentation


---

## 📊 Key Results

- **Final Model:** Calibrated LightGBM  
- **Test ROC-AUC:** ~0.83  
- **LogLoss:** ~0.50  
- **Brier Score:** ~0.16 (improved after isotonic calibration)  

### Threshold Scenarios  
- **0.30 (High Recall):** ~64% recall, ~53% precision — fewer missed defaults.  
- **0.45 (KS point):** ~23% recall, ~85% precision — fewer false alarms, more balanced.  

📈 **Recommendation:**  
Use **0.30** as operational cutoff (recall priority).  
Fallback to **0.45 (KS point)** if resources are constrained.  

---

## 🔎 Interpretability

- **Global Drivers (SHAP):**  
  - Interest Rate ↑ → higher default risk  
  - Loan Amount ↑ → higher risk  
  - Total BC Limit ↑ → lower risk  
  - Funded Amount ↑ → higher risk  

- **Local Explanations (SHAP):**  
  - Each high-risk borrower gets top 3 SHAP drivers explaining risk score.  
  - Risk teams understand *why* a borrower is flagged, not just the probability.  

---

## 🚀 Future Work

- **Modeling Enhancements:** Explore CatBoost, neural networks, cost-sensitive learning.  
- **Feature Engineering:** Add temporal payment histories, macroeconomic indicators.  
- **Deployment:** Streamlit / Dash dashboards, batch scoring pipelines, API integration.  
- **Business Strategy:** Use probability scores for approval, pricing, collections, and regulatory reporting.  

---

## 📦 Reproducibility

Artifacts saved in `models/` directory ensure reproducibility:  

- Preprocessor (`preprocessor_final.joblib`)  
- Final Calibrated LightGBM (`lgbm_model_calibrated.joblib`)  
- Metadata (`metadata_final.json`)  
- Risk Report (`default_risk_report.csv`)  

Run notebooks in order (1 → 2 → 3) to reproduce results.  

⚠️ **Note:** Do not flip `USE_SAMPLE=False` in Notebook 1 unless running on a machine with >6 GB memory.  
A full processed dataset (`loan_default_full51.parquet`) is already provided.  

---

## ⚡ Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/<your-username>/loan-default-probability.git
cd loan-default-probability

### 2. Create & Activate Environment

conda create -n loan_default python=3.11 -y
conda activate loan_default

### 3. Install Requirements

pip install -r requirements.txt

### 4. Run Notebooks

jupyter lab

Run in order:

1_data_wrangling_EDA.ipynb

2_preprocessing_training.ipynb

3_modeling_results.ipynb

### 5. Inspect Artifacts

Saved models & reports are in the models/ directory.

🎯 Conclusion

This project delivers a production-ready, explainable loan default probability model.

It empowers risk managers to:

Flag high-risk borrowers early

Adjust thresholds by resource and business constraints

Understand why defaults are predicted via SHAP interpretability

The result is a data-driven decision-support system for credit risk management and compliance.

## ⚠️ Memory Warning

The raw LendingClub dataset is **large (>2.4 GB compressed, ~6 GB in-memory)**.  

- Always work with the **sample (`loan_default_slim55.parquet`)** during exploration.  
- The **full dataset (`loan_default_full51.parquet`)** has already been reduced to 51 features and saved for you.  
- **Do not flip `USE_SAMPLE=False` inside Notebook 1** — this will attempt to load the raw CSV and crash most local machines.  
Instead, rely on the pre-saved parquet files.

