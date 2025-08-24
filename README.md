# P8-Bank-Marketing-Campaign-Analysis

**Version 1 - Dataset 1 - Predictive Analysis**

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

**Version 2 - Dataset 2 - Descriptive Analysis**

**A. Project Overview**

- The project aims to identify the best strategies to improve for the next marketing campaign by analyzing the last marketing campaign, identify the patterns that will help us find conclusions in order to develop future strategies.

![Dashboard Visualization](Version%202%20-%20Descriptive%20Analysis%20%28Dataset%202%29/Visualization/Overview.png)

**B. Dataset Information**

**I. Source**

- From: UCI Machine Learning Repository
https://archive.ics.uci.edu/dataset/222/bank+marketing
- Rows: 41,188
- Columns: 20 (input variables) + 1 (target: y)

**II. Variable Description**

**1. Customer Profile**
- age (numeric)
- job : type of job (categorical: "admin.","blue-collar","entrepreneur","housemaid","management","retired","self-employed","services","student","technician","unemployed","unknown")
- marital : marital status (categorical: "divorced","married","single","unknown"; note: "divorced" means divorced or widowed)
- education (categorical: "basic.4y","basic.6y","basic.9y","high.school","illiterate","professional.course","university.degree","unknown")
- default: has credit in default? (categorical: "no","yes","unknown")
- housing: has housing loan? (categorical: "no","yes","unknown")
- loan: has personal loan? (categorical: "no","yes","unknown")

**Related with the last contact of the current campaign**
- contact: contact communication type (categorical: "cellular","telephone") 
- month: last contact month of year (categorical: "jan", "feb", "mar", ..., "nov", "dec")
- day_of_week: last contact day of the week (categorical: "mon","tue","wed","thu","fri")
- duration: last contact duration, in seconds (numeric). Important note:  this attribute highly affects the output target (e.g., if duration=0 then y="no"). Yet, the duration is not known before a call is performed. Also, after the end of the call y is obviously known. Thus, this input should only be included for benchmark purposes and should be discarded if the intention is to have a realistic predictive model.

**Other attributes**
- campaign: number of contacts performed during this campaign and for this client (numeric, includes last contact)
- pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric; 999 means client was not previously contacted)
- previous: number of contacts performed before this campaign and for this client (numeric)
- poutcome: outcome of the previous marketing campaign (categorical: "failure","nonexistent","success")

**Social and economic context attributes**
- emp.var.rate: employment variation rate - quarterly indicator (numeric)
- cons.price.idx: consumer price index - monthly indicator (numeric)     
- cons.conf.idx: consumer confidence index - monthly indicator (numeric)     
- euribor3m: euribor 3 month rate - daily indicator (numeric)
- nr.employed: number of employees - quarterly indicator (numeric)

**Output variable (desired target)**

- y - has the client subscribed a term deposit? (binary: "yes","no")

**C. Methodology**

**I. Key Findings**

_**_1. Executive Overview_**_
- The overall conversion rate is relatively low (~11%), below the industry benchmark (best-in-class banking campaigns can reach ~15%).
→ The bank has no competitive advantage yet and needs to optimize targeting and contact strategy significantly.

**_2. Customer profile_**
- Age: Customers aged 25–44 are the most likely to subscribe. The 45–54 group follows but only accounts for ~64% of the 25–44 group’s subscriptions.
- Occupation: Admin, Blue-collar, and Technician represent the top subscribing occupations.
- Marital status: Married customers nearly double the subscriptions compared to single or divorced ones.
- Education: University and High school customers have the highest subscription numbers.
- Financial profile:
  + Customers without credit in default are ~3.7x more likely to subscribe than those with defaults.
  + Customers with a house are ~1.2x more likely than those without.
  + Customers without a personal loan are ~5.7x more likely than those with loans.

**_3. Last Contact_**
- Channel: Contacting customers via cellular is ~1.7x more effective than telephone.
- Timing:
  + May is the peak month for subscriptions (~2x higher than July, the second-highest).
  + Day of the week shows little variation → efforts can be spread evenly.
  + Duration: Calls lasting 61–300s are ~2.6x more likely to succeed than longer calls (301–900s).

**_4. Other Attributes_**
- Campaign frequency: Contrary to intuition, the more times a customer is contacted, the lower the conversion rate
- Pdays: Customers who were never contacted in the current campaign are ~40x more likely to subscribe.
- Previous campaigns: Customers who had never participated in earlier campaigns are ~7.7x more likely to subscribe.
- Poutcome: Almost no customers who subscribed in a previous campaign subscribed again → very weak retention.

**II. Actionable plans**
- Target younger to mid-career, married customers with stable occupations, higher education, and fewer financial liabilities.
- Prioritize cellular channel, intensify campaigns in May, and standardize call scripts to last between 1–5 minutes.
- Limit over-contacting (avoid spam), prioritize fresh leads & establish dedicated retention strategies for past subscribers.

**E. About Me**

Hi, I'm Navin (Bao Vy) – an aspiring Data Analyst passionate about turning raw data into actionable business insights. I’m eager to contribute to data-driven decision making and help organizations translate analytics into business impact. For more details, please reach out at:

🌐 LinkedIn: https://www.linkedin.com/in/navin826/

📂 Portfolio: https://github.com/CallmeNavin/
