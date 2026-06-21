Heart Disease Prediction using Supervised Machine Learning
COEN807 Term Project — Ahmadu Bello University, Zaria, June 2026
� � �
Project Overview
This project builds an end-to-end supervised machine learning pipeline to predict the presence of heart disease from 13 clinical and demographic features. Five classifiers are trained, evaluated under 5-fold stratified cross-validation, and compared on a held-out test set using AUC-ROC as the primary metric.
Best result: K-Nearest Neighbours — AUC-ROC = 0.733 on held-out test set.
Dataset
Source: Modelled on the UCI Cleveland Heart Disease Dataset
Samples: 303 patients
Features: 13 clinical variables (age, sex, chest pain type, cholesterol, max heart rate, etc.)
Target: Binary — 1 = Heart disease present, 0 = Absent
Class distribution: 79.2% negative / 20.8% positive
The dataset CSV is included in this repository at data/heart_disease_dataset.csv.
Repository Structure
COEN807-Heart-Disease-ML/
│
├── data/
│   └── heart_disease_dataset.csv       # 303-patient dataset
│
├── results/
│   ├── fig1_eda_distribution.png
│   ├── fig2_correlation.png
│   ├── fig3_feature_boxplots.png
│   ├── fig4_roc_curves.png
│   ├── fig5_confusion_matrix.png
│   ├── fig6_model_comparison.png
│   ├── fig7_feature_importance.png
│   ├── fig8_cv_comparison.png
│   └── model_metrics.csv               # Final accuracy + AUC-ROC per model
│
├── report/
│   └── COEN807_Heart_Disease_Report.docx
│
├── slides/
│   └── COEN807_Presentation.pptx
│
├── train.py                            # Main ML pipeline (run this)
├── requirements.txt
└── README.md
Quickstart
1. Clone the repository
git clone https://github.com/P25ECGP8066/COEN807-Heart-Disease-ML.git
cd COEN807-Heart-Disease-ML
2. Install dependencies
pip install -r requirements.txt
3. Run the full pipeline
python train.py
This single command will:
Load and inspect the dataset
Generate all 8 EDA and results figures → saved to results/
Train 5 classifiers under 5-fold stratified cross-validation
Run hyperparameter grid search on Gradient Boosting
Print CV AUC-ROC scores and test-set metrics
Save results/model_metrics.csv
Expected runtime: ~60 seconds on a standard laptop CPU.
Models Evaluated
Model
CV AUC (Mean ± Std)
Test AUC
Test Accuracy
Logistic Regression
0.671 ± 0.040
0.697
77.0%
Random Forest
0.589 ± 0.052
0.662
75.4%
Gradient Boosting
0.568 ± 0.097
0.599
72.1%
SVM (RBF)
0.615 ± 0.051
0.649
78.7%
KNN (K=7)
0.572 ± 0.069
0.733
78.7%
GBM (Tuned)
—
0.625
77.0%
Key Findings
KNN achieved the highest test AUC (0.733), suggesting local geometric structure is informative in this scaled feature space.
Tree ensembles underperformed relative to expectations — likely due to limited dataset size (N=303).
Top predictors (Random Forest importance): max heart rate (thalach), ST depression (oldpeak), number of coloured vessels (ca).
Clinical safety concern: Disease-class recall is low (0.08). Threshold calibration below 0.5 is required before any clinical deployment.
Reproducibility
All random seeds are fixed at 42. The scikit-learn Pipeline object ensures StandardScaler is fit only on training data — no data leakage. Results are deterministic across runs.
Python version tested: 3.10, 3.11
OS tested: Ubuntu 22.04, macOS 14
Ethical Considerations
This model is for academic purposes only and must not be used for clinical diagnosis.
The dataset is from a single US hospital (1988) and may not generalise to other populations.
A false negative (missing a disease case) carries high clinical cost — any deployment must involve threshold calibration, fairness auditing, and prospective clinical validation.
References
Detrano, R. et al. (1989). International application of a new probability algorithm for the diagnosis of coronary artery disease. The American Journal of Cardiology, 64(5), 304–310.
Pedregosa, F. et al. (2011). Scikit-learn: Machine Learning in Python. JMLR, 12, 2825–2830.
Breiman, L. (2001). Random Forests. Machine Learning, 45(1), 5–32.
Friedman, J. H. (2001). Greedy function approximation: a gradient boosting machine. Annals of Statistics, 29(5), 1189–1232.
Author
Abdulkarim Ibrahim
Student ID: P25ECGP8066
COEN807 — Machine Learning
Ahmadu Bello University, Zaria, June 2026
