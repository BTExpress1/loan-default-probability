## 📓 Project Notebooks

This project is structured into three main notebooks, each serving a distinct role in the pipeline:

1. **Notebook 1 — Data Wrangling & EDA**
   - Load LendingClub dataset (2.4GB raw → sampled for EDA).  
   - Cleaned and reduced features (145 → 117 → 80 → 54).  
   - Explored target distribution and probability views.  
   - Saved final feature set (`columns_to_keep.txt`) for reproducibility.

2. **Notebook 2 — Preprocessing & Baseline Modeling**
   - Apply encoding (categorical → one-hot/label).  
   - Apply scaling (Robust/Standard for skewed numerics).  
   - Train baseline models (Logistic Regression, Random Forest, XGBoost).  
   - Evaluate using ROC-AUC, LogLoss, precision/recall curves.  
   - Address class imbalance with class weights/resampling.  

3. **Notebook 3 — Tuning, Calibration & Business Insights**
   - Hyperparameter optimization with cross-validation.  
   - Model calibration (e.g., isotonic) to improve probability estimates.  
   - Feature importance with SHAP values.  
   - Business-facing outputs: threshold scenarios, KS statistic cutoffs.  
   - Generate interpretable insights for HR/compliance teams.
     

---

📌 **Tip:** Run the notebooks in order (1 → 2 → 3). Artifacts from one notebook (cleaned data, selected features, saved models) feed into the next for full reproducibility.

## Project Setup / Data Handling

## ⚠️ Memory Warning

The raw LendingClub dataset is **large (>2.4 GB compressed, ~6 GB in-memory)**.  

- Always work with the **sample (`loan_default_slim55.parquet`)** during exploration.  
- The **full dataset (`loan_default_full55.parquet`)** has already been reduced to the same 54 features and saved for you.  
- **Do not flip `USE_SAMPLE=False` inside Notebook 1** — this will attempt to load the raw CSV and crash most local machines.  
Instead, rely on the pre-saved parquet files.

