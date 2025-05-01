# DonorsChoose Project Funding Prediction

This project uses machine learning to predict whether educational projects posted on DonorsChoose.org will be fully funded. By identifying the projects least likely to be funded, we aim to support more equitable and data-driven resource allocation in K-12 education.

---

##  Contributors

- Anshika Shukla  
- Tiffany Gan  
- Zihan Liu

---

## 📁 Repository Contents

| File/Folder                      | Description                                                                 |
|----------------------------------|-----------------------------------------------------------------------------|
| `mlp_updated.ipynb`              | Full Jupyter notebook with EDA, feature engineering, modeling, and bias audit |
| `data/`                          | Datasets used for our project (see Kaggle instructions below)              |
| `feature_matrix.csv`             | Final cleaned and encoded dataset used for model training(auto-generated when run)     |
| `projects_for_expert_review.csv` | Bottom 10% least likely funded projects, based on model predictions (auto-generated)       |
| `df.csv`                         | Cleaned and merged dataset before encoding (auto-generated)          |
| `README.md`                      | Project overview, structure, and setup instructions                        |

>  **Important**: You will need to manually download the following datasets from [Kaggle - KDD Cup 2014](https://www.kaggle.com/competitions/kdd-cup-2014-predicting-excitement-at-donors-choose/data) and place them in the `data/` folder:

- `donations.csv`  
- `essays.csv`  
- `projects.csv`  
- `resources.csv`  
- `outcomes.csv`  

---

##  Setup Instructions

###  Prerequisites

- Python 3.8 or newer  
- Jupyter Notebook or JupyterLab  
- Git (for repository cloning)  
- (Optional) Anaconda for environment management  

###  Required Python Packages

You can install the dependencies using:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn xgboost lightgbm shap
```

---

## Problem Statement

Teachers in under-resourced U.S. schools post projects requesting materials for their classrooms. However, not all projects get funded. Our goal is to:

- Predict which projects are less likely to be fully funded  
- Surface these projects for early intervention or expert review  
- Audit the model for biases across school demographics  

---

##  Data Sources

[DonorsChoose KDD Cup 2014 Dataset](https://www.kaggle.com/competitions/kdd-cup-2014-predicting-excitement-at-donors-choose/data)

- `projects.csv`: Project and teacher metadata  
- `essays.csv`: Project narratives  
- `outcomes.csv`: Binary label for whether a project was funded  
- `donations.csv`: Aggregated donation activity  
- `resources.csv`: Requested items and cost breakdowns  

---

##  Data Preprocessing

- Merged multiple tables on `projectid`  
- Engineered features from:
  - Essay text lengths  
  - Resource costs and item types  
  - School location and metadata  
  - Time-based variables (month/year posted)  
- Removed columns with >40% missing values  
- Applied SMOTE to balance the dataset  

---

##  Modeling Approach

We trained and evaluated the following classifiers:

- Logistic Regression  
- Random Forest  
- Gradient Boosting  
- SGD Classifier  
- K-Nearest Neighbors  
- XGBoost (**best performance**)  
- LightGBM  

**Evaluation Metrics:**
- ROC AUC  
- Precision, Recall, F1-score for "Not Funded" class  
- ROC Curve Visualization  

---

##  Key Results

The top-performing model, **LightGBM**, achieved:
- **AUC**: 0.85  
- **Recall**: 80% (on the “Not Funded” class)

This allows DonorsChoose experts to focus their daily review efforts on the bottom 10% most at-risk projects.

---

## Bias Audit

Audited fairness across:
- `poverty_level`  
- `grade_level`  
- `school_state`  

**Findings:**
- Better performance on high-income schools  
- Lower accuracy in states like OK, NM, and HI  

---

## Expert Review List

We ranked projects by predicted probability and exported the **bottom 10%** to `projects_for_expert_review.csv` for manual review and potential intervention.

---

##  Future Improvements

- Incorporate **sentiment analysis** to capture emotional tone in essays  
- Emphasize **features available at posting time** for real-time usability  
- Build a **teacher dashboard** with risk scores and revision guidance
