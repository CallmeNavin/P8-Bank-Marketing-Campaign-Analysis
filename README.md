# P8-Bank-Marketing-Campaign-Analysis

**Version 1 - Dataset 1**

**A. Project Overview**

- The project aims to identify the best strategies to improve for the next marketing campaign by analyzing the last marketing campaign, identify the patterns that will help us find conclusions in order to develop future strategies.


**B. Dataset Information**

**Source**

From: Bank Marketing Dataset (Kaggle)
https://www.kaggle.com/datasets/janiobachmann/bank-marketing-dataset/data

**Disclaimer:**

- In this dataset, the target variable (deposit) has been oversampled and balanced, resulting in an unusually high proportion of positive cases (46%).
- This distribution does not reflect the real-world deposit rate (≈11% in the original dataset).
- Therefore, this dataset is intended for machine learning practice (predictive modeling), not for deriving business insights or action plans.
- In another version (Version 2 - Dataset 2), we will use another dataset to explore business insights and action plans more aligned with real-world scenarios.

**C. Methodology**

**I. Logistic Regression**

_**1. Objective**_

Logistic Regression was used as the baseline model to classify whether a client subscribes to a term deposit (deposit = 1) or not (deposit = 0). It was selected for its simplicity, interpretability, and frequent use as a benchmark in classification problems.

_**2. Approach**_

- Features were preprocessed with one-hot encoding for categorical variables and numeric variables were kept as is. The target variable was deposit.
- Logistic Regression was trained with an increased number of iterations to ensure convergence. Since the dataset is relatively balanced (deposit rate = 46%), no class weighting was applied.

_**3. Results**_

- Precision (deposit = Yes) = 0.71
- Recall (deposit = Yes) = 0.63
- F1-score (deposit = Yes) = 0.67
- Accuracy = 0.71
- ROC-AUC = 0.70
- Average Precision score = 0.62

_**4. Evaluation**_

- The model achieves a balanced trade-off between Precision and Recall for the positive class (deposit).
- An ROC-AUC of 0.70 shows the model can distinguish between deposit vs. non-deposit clients significantly better than random (0.5).
- The Average Precision score of 0.62 is also notably higher than the baseline positive rate (0.46), confirming that the model captures meaningful patterns.
→ Although simple, Logistic Regression provides a reliable baseline to compare with more complex models such as Random Forest or XGBoost.

_**5. Next Steps**_

While Logistic Regression provides a solid baseline, further steps will be taken to improve model performance and derive actionable business insights

**II. Random Forest Classifier**

_**1. Objective**_

Random Forest was applied as the next model to compare against the Logistic Regression baseline. It was chosen because of its ability to capture non-linear relationships and feature interactions, which Logistic Regression may fail to model.

_**2. Approach**_

- The same preprocessed dataset was used, with one-hot encoded categorical variables and numeric variables kept as is.
- Random Forest was trained with 300 decision trees (n_estimators=300) to ensure model stability.
- Hyperparameters were lightly tuned to reduce overfitting: min_samples_split=10, min_samples_leaf=5, max_features='sqrt'.
- No class weighting was applied, since the dataset is relatively balanced (deposit rate ≈ 46%).

_**3. Results**_

- Precision (deposit = Yes) = 0.76
- Recall (deposit = Yes) = 0.59
- F1-score (deposit = Yes) = 0.66
- Accuracy = 0.72
- ROC-AUC = 0.71
- Average Precision score = 0.64

_**4. Evaluation**_

- Compared to Logistic Regression, Random Forest achieved higher Precision but slightly lower Recall on the positive class (deposit).
- ROC-AUC and PR-AUC both improved, indicating stronger overall discriminative power.
→ Random Forest is better at ranking customers by deposit likelihood, but at the cost of missing some true depositors (lower Recall). The trade-off suggests Random Forest is more suitable in cases where targeting fewer but more likely clients is preferred, e.g., marketing campaigns with limited call budgets.

_**5. Next Steps Enhancement**_

- Perform systematic hyperparameter tuning (GridSearchCV / RandomizedSearchCV) to explore deeper improvements.
- Compare Random Forest with gradient boosting methods (XGBoost, LightGBM), which often outperform both Logistic Regression and Random Forest in structured tabular data.
- Extend the evaluation with business-oriented metrics such as Precision@k and Lift@k to simulate campaign targeting efficiency.

_**III. Evaluation**_

Overall, Random Forest demonstrates incremental improvements over Logistic Regression, though the optimal choice depends on business priorities (higher precision vs. higher recall). The model will continue to be enhanced and benchmarked against more advanced methods over time.

**D. About Me**

Hi, I'm Navin (Bao Vy) – an aspiring Data Analyst passionate about turning raw data into actionable business insights. I’m eager to contribute to data-driven decision making and help organizations translate analytics into business impact. For more details, please reach out at:

🌐 LinkedIn: https://www.linkedin.com/in/navin826/

📂 Portfolio: https://github.com/CallmeNavin/
