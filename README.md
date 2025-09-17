# Biomarkers in Neuronal Synuclein Disease (NSD)

A reproducible notebook-driven analysis exploring potential **biomarkers** for Neuronal Synuclein Disease (NSD). 
This repo focuses on data prep, model training/evaluation, and clear visualizations (correlations, feature importance, ROC/PR curves, and confusion matrices).

---

## Contents

- `Biomarkers in Neuronal Synuclein Disease.ipynb` — main analysis notebook.
- `Biomarkers in Neuronal Synuclein Disease.html` — HTML export of the notebook.
- `Biomarkers in Neuronal Synuclein Disease for pdf.html` — HTML formatted for printing/PDF.
- `SAA_Biospecimen_Analysis_Results.csv` — biospecimen dataset used in the notebook (update this description as needed).
- `requirements.txt` — pinned Python dependencies to reproduce the environment.

---

## Getting Started

### 1) Clone
```bash
git clone https://github.com/jcjaylani/Biomarkers_in_NSD.git
cd Biomarkers_in_NSD
```

### 2) Create environment (recommended)
Using **venv**:
```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate
```

Or using **conda**:
```bash
conda create -n nsd python=3.11 -y
conda activate nsd
```

### 3) Install requirements
```bash
pip install -r requirements.txt
```

### 4) Run the notebook
```bash
jupyter notebook "Biomarkers in Neuronal Synuclein Disease.ipynb"
```
Or open with **JupyterLab**.

---

## Data

- Default dataset: `SAA_Biospecimen_Analysis_Results.csv` (CSV).  
- Update paths in the notebook if you store data elsewhere.
- Ensure the target/label column name used in the notebook matches your dataset.

---

## Visualizations (from the notebook)

Below are code snippets used in the notebook to standardize key plots. 
You can paste these into your own scripts/notebooks if needed.

### 1) Correlation heatmap
```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(10, 8))
sns.heatmap(df.corr(numeric_only=True), cmap="coolwarm", center=0, square=False)
plt.title("Correlation Heatmap of Biomarkers")
plt.tight_layout()
plt.show()
```

### 2) Feature importance (RandomForest)
```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

rf.fit(X_train, y_train)
importances = rf.feature_importances_
indices = np.argsort(importances)[::-1][:20]  # top 20
top_features = X_train.columns[indices]

plt.figure(figsize=(10, 6))
sns.barplot(x=importances[indices], y=top_features)
plt.xlabel("Importance")
plt.ylabel("Feature")
plt.title("Top 20 Feature Importances (Random Forest)")
plt.tight_layout()
plt.show()
```

### 3) ROC curve
```python
from sklearn.metrics import roc_curve, auc
import matplotlib.pyplot as plt

y_score = rf.predict_proba(X_test)[:, 1]
fpr, tpr, _ = roc_curve(y_test, y_score)
roc_auc = auc(fpr, tpr)

plt.figure()
plt.plot(fpr, tpr, label=f"Random Forest (AUC = {roc_auc:.2f})")
plt.plot([0, 1], [0, 1], "k--", lw=1)
plt.xlabel("False Positive Rate")
plt.ylabel("True Positive Rate")
plt.title("ROC Curve")
plt.legend(loc="lower right")
plt.tight_layout()
plt.show()
```

### 4) Precision–Recall curve
```python
from sklearn.metrics import precision_recall_curve, average_precision_score
import matplotlib.pyplot as plt

y_score = rf.predict_proba(X_test)[:, 1]
precision, recall, _ = precision_recall_curve(y_test, y_score)
ap = average_precision_score(y_test, y_score)

plt.figure()
plt.plot(recall, precision, label=f"Random Forest (AP = {ap:.2f})")
plt.xlabel("Recall")
plt.ylabel("Precision")
plt.title("Precision–Recall Curve")
plt.legend()
plt.tight_layout()
plt.show()
```

### 5) Confusion matrix
```python
from sklearn.metrics import confusion_matrix
import seaborn as sns
import matplotlib.pyplot as plt

y_pred = rf.predict(X_test)
cm = confusion_matrix(y_test, y_pred)

plt.figure(figsize=(4, 4))
sns.heatmap(cm, annot=True, fmt="d", cmap="Blues", cbar=False)
plt.xlabel("Predicted")
plt.ylabel("Actual")
plt.title("Confusion Matrix — Random Forest")
plt.tight_layout()
plt.show()
```

---

## Modeling Notes

- Preprocessing utilities used: `SimpleImputer`, `StandardScaler` / `MinMaxScaler`.
- Classifiers explored: `RandomForestClassifier`, `DecisionTreeClassifier` (extend as needed).
- Metrics covered: `accuracy_score`, `roc_auc_score`, `classification_report`, calibration via `calibration_curve`.
- For class imbalance, **SMOTE** (`imblearn.over_sampling.SMOTE`) can improve minority class learning. 
  Use it **only on the training set** inside cross-validation to avoid leakage.

---

## Project Structure
```
Biomarkers_in_NSD/
├─ Biomarkers in Neuronal Synuclein Disease.ipynb
├─ Biomarkers in Neuronal Synuclein Disease.html
├─ Biomarkers in Neuronal Synuclein Disease for pdf.html
├─ SAA_Biospecimen_Analysis_Results.csv
├─ requirements.txt
└─ docs/ or assets/           # (optional) save figures here
```

---

## Contributing

Issues and PRs are welcome: open a discussion for features (e.g., new biomarkers, models, or evaluation methods).

---

## Citation

If this repo contributes to your research, please cite:
> Jaylani, J. (2025). Biomarkers in Neuronal Synuclein Disease (NSD). GitHub repository: https://github.com/jcjaylani/Biomarkers_in_NSD

