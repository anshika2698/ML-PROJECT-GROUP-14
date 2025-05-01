This project uses machine learning to predict whether educational projects posted on DonorsChoose.org will be fully funded. By identifying the projects least likely to be funded, we aim to support more equitable and data-driven resource allocation in K-12 education.

## Contributors

- Anshika Shukla
- Tiffany Gan
- Zihan Liu

## Repository Contents

| File/Folder                    | Description                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| `mlp.ipynb`                   | Full Jupyter notebook with EDA, feature engineering, modeling, and bias audit |
| `data`                        | datasets used for our projects, instruction below                              |
| `feature_matrix.csv`          | Final cleaned and encoded dataset used for model training                    |
| `projects_for_expert_review.csv` | Bottom 10% least likely funded projects, based on model predictions     |
| `df.csv`                      | Cleaned and merged dataset before encoding                                  |
| `README.md`                   | Project overview, structure, and setup instructions                         |

> To run this project, you will need to manually download the following datasets from [Kaggle - KDD Cup 2014](https://www.kaggle.com/competitions/kdd-cup-2014-predicting-excitement-at-donors-choose/data):

- `donations.csv`
- `essays.csv`
- `projects.csv`
- `resources.csv`
- `outcomes.csv`

Place them in the same directory as our jupyter notebook file.


---

## Setup Instructions

### Prerequisites

Before running the notebook, ensure the following are installed:

- Python 3.8 or newer  
- Jupyter Notebook or JupyterLab  
- Git (for repository cloning)  
- (Optional) Anaconda for environment management  

### Required Python Packages

You can install the dependencies using pip:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn xgboost lightgbm shap


## Problem Statement

Teachers in under-resourced U.S. schools post projects requesting materials for their classrooms. However, not all projects get funded. Our goal is to:

- Predict which projects are less likely to be fully funded
- Surface these projects for early intervention or expert review
- Audit the model for biases across school demographics

## Data Sources
https://www.kaggle.com/competitions/kdd-cup-2014-predicting-excitement-at-donors-choose/data
- projects.csv: Project and teacher metadata
- essays.csv: Project narratives
- outcomes.csv: Binary label for whether a project was funded
- donations.csv: Aggregated donation activity
- resources.csv: Requested items and cost breakdowns

## Data Preprocessing

- Merged multiple tables on projectid
- Engineered features from:
  - Essay text lengths
  - Resource costs and item types
  - School location and metadata
  - Time-based variables (month/year posted)
- Removed columns with >40% missing values
- Applied SMOTE to balance the dataset

## Modeling Approach

We trained and evaluated the following classifiers:

- Logistic Regression
- Random Forest
- Gradient Boosting
- SGD Classifier
- K-Nearest Neighbors
- XGBoost (best performance)
- LightGBM

Each model was assessed using:
- ROC AUC
- Precision, Recall, F1-score for "Not Funded" class
- ROC Curve Visualization

## Key Results

Our top-performing model, LightGBM, achieved an AUC of 0.85 and Recall of 80% for the “Not Funded” class, effectively identifying at-risk projects. This enables DonorsChoose experts to focus their limited daily capacity on the 10% of proposals least likely to be funded, improving intervention targeting and platform efficiency. Our model also demonstrated disparities across states and poverty levels, which we addressed through a bias audit.


## Bias Audit

We evaluated model fairness across:
- poverty_level
- grade_level
- school_state

Findings:
- Model performs better on high-income schools (risk of under-prioritizing low-income areas)
- Some states like OK, NM, HI showed worse prediction performance

## Expert Review List

We ranked all test projects by predicted funding probability and exported the bottom 10% to projects_for_expert_review.csv. These projects can be surfaced for manual review, outreach, or intervention.

## Future Improvements

To improve the model further, we plan to:
Incorporate sentiment analysis to capture emotional tone and urgency in essays, beyond just text length.
Focus more on features available at posting time to make predictions usable for real-time interventions.
Build a teacher-facing dashboard explaining why a project is at-risk and offering tips for improvement.

