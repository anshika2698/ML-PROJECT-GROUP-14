This project uses machine learning to predict whether educational projects posted on DonorsChoose.org will be fully funded. By identifying the projects least likely to be funded, we aim to support more equitable and data-driven resource allocation in K-12 education.

## Project Structure

mlp.ipynb            - Jupyter notebook file for our project
outputs/
├── feature_matrix.csv - Final cleaned and encoded dataset
├── projects_for_expert_review.csv - Bottom 10% projects (lowest predicted funding probability)
└── model_metrics.png  - ROC curves and evaluation plots
README.md              - Project overview and instructions

## Problem Statement

Teachers in under-resourced U.S. schools post projects requesting materials for their classrooms. However, not all projects get funded. Our goal is to:

- Predict which projects are less likely to be fully funded
- Surface these projects for early intervention or expert review
- Audit the model for biases across school demographics

## Data Sources

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



## Contributors

- Anshika Shukla
- Tiffany Gan
- Zihan Liu