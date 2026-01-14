# Telecom Customer Churn Prediction
________________________________________
## 1. Project Overview
No-Churn Telecom is an established telecom operator facing increased customer churn due to high market competition. This project aims to leverage Machine Learning techniques to identify customers likely to churn and enable targeted retention strategies.
________________________________________
## 2. Business Objectives
- Identify key factors influencing customer churn
- Predict churn probability for each customer
- Generate actionable churn risk indicators for retention campaigns
________________________________________
## 3. Data Description
The dataset was sourced from No-Churn Telecom’s SQL database containing 4,617 customer records. It includes customer demographics, usage patterns, billing information, and service interaction data.
________________________________________
## 4. Exploratory Data Analysis (EDA)
EDA revealed that customer service calls, international plan usage, and higher call charges are strong indicators of churn. The dataset showed class imbalance, justifying the use of ROC-AUC, Recall, and F1-score for model evaluation.

### 4.1 Target Variable Distribution
•	The dataset shows a clear class imbalance, with the majority of customers labeled as Non-Churn (No).
•	Approximately 10–15% of customers have churned, which aligns with the business concern highlighted by No-Churn Telecom.
•	This imbalance indicates that accuracy alone is not sufficient for model evaluation.
•	Metrics such as Recall, F1-score, and ROC-AUC are more appropriate to measure churn prediction performance.
•	The observed churn rate confirms the need for targeted retention strategies rather than blanket offers.

### 4.2 Categorical Feature Analysis vs Churn
International Plan vs Churn
•	Customers with International Plan = Yes show higher churn
•	Indicates pricing dissatisfaction or competitor offers
Voice Mail Plan vs Churn
•	Voice Mail Plan users are more stable
•	Indicates higher engagement and service stickiness
4.3 Numerical Feature Distribution
Customer Service Calls
•	Churned customers make significantly more service calls
•	Strong indicator of dissatisfaction
•	High-impact retention trigger
Day Minutes Usage
•	High day usage customers churn more
•	Possible billing shock or tariff issues
Correlation Analysis
•	Strong correlation between:
o	Minutes ↔ Charges (expected)
•	Customer service calls strongly linked to churn
•	No extreme multicollinearity issues
Modeling Justification - EDA supports:
•	Tree-based models (non-linear relationships)
•	Random Forest as final model
•	Churn probability scoring for campaigns
________________________________________
## 5. Data Preprocessing
Data preprocessing was performed using a ColumnTransformer pipeline. Numerical features were scaled using StandardScaler, while categorical variables were encoded using OneHotEncoder. Target labels were cleaned and encoded appropriately.
________________________________________
## 6. Model Building & Evaluation
Multiple machine learning models were evaluated, including Logistic Regression, Decision Tree, Random Forest, Gradient Boosting, HistGradientBoosting, and XGBoost. Models were compared using ROC-AUC, Recall, Precision, and F1-score.
________________________________________
## 7. Model Selection

### 7.1 Interpretation of Evaluation Graphs
7.1.1️. ROC Curve Comparison
•	Random Forest shows the highest ROC-AUC (0.738), indicating the best overall ability to distinguish between churned and non-churned customers.
•	Gradient Boosting and XGBoost follow closely but do not surpass Random Forest.
•	Logistic Regression performs worst in overall discrimination.
7.1.2️. ROC-AUC vs Recall Bar Chart
•	Logistic Regression achieves the highest recall, but at the cost of:
o	Very low precision
o	Higher false positives
•	Random Forest provides a balanced trade-off between recall and precision.
•	Boosting models show strong precision but comparatively lower recall.

### 7.2 Business-Oriented Model Selection Logic
In a telecom churn scenario:
•	Recall is important → missing a churner is costly
•	But precision also matters → too many false churn alerts waste retention resources
•	Therefore, the goal is balanced performance, not extreme recall or precision alone

### 7.3 Final Model Selected: Random Forest
Why Random Forest was chosen:
1.	Highest ROC-AUC (0.738)
o	Best overall discriminatory power among all models
2.	Balanced Recall and Precision
o	Captures a significant portion of churners
o	Avoids excessive false positives compared to Logistic Regression
3.	Best F1-score (0.387)
o	Indicates the strongest balance between precision and recall
4.	Model Stability & Interpretability
o	Less sensitive to noise than single trees
o	Feature importance can be easily explained to business teams
5.	Operational Suitability
o	Robust for real-world deployment
o	Performs well without aggressive hyperparameter tuning

### 7.4 Why Other Models Were Not Selected
-	Logistic Regression
  -	High recall but poor precision
  -	Leads to excessive false churn alerts
- XGBoost / Gradient Boosting
  - Strong precision but lower recall
  - Misses a higher number of churn customers
- Decision Tree
  -	Simpler but less stable and lower overall performance
-	HistGradientBoosting
  -	Efficient but weaker performance compared to Random Forest
________________________________________
## 8. Feature Importance
Feature importance analysis highlights the variables that most strongly influence customer churn predictions. The results indicate that customer service interactions, usage patterns, and billing-related variables play a significant role in determining churn behavior. Customers with a higher number of customer service calls tend to show a greater likelihood of churn, suggesting dissatisfaction with service quality or issue resolution
Usage and charge-related features, such as call minutes and corresponding charges, also contribute notably to churn risk, indicating potential price sensitivity among heavy users. Additionally, service plan features, including international and voicemail plans, influence customer retention, reflecting differences in engagement and perceived value.
Overall, the feature importance results provide actionable insights that can help the business focus retention efforts on high-impact areas such as improving customer support, optimizing pricing strategies, and tailoring service plans for at-risk customers.
________________________________________
## 9. Churn Risk Scoring
Instead of binary predictions, churn probabilities were converted into risk bands (Low, Medium, High). This enables prioritized and cost-effective retention actions.

### 9.1 Churn Risk Analysis (Interpretation)
•	The displayed customers have churn probabilities in the range of ~0.43–0.49, which places them in the Medium Risk category.
•	These customers are not certain churners, but they exhibit noticeable risk signals compared to low-risk users.
•	Medium-risk customers typically represent the largest opportunity group for retention, as timely interventions can prevent escalation to high risk.
•	Recommended actions for this segment include:
o	Personalized offers or plan optimization
o	Proactive communication (email/SMS/app notifications)
o	Monitoring service experience to avoid dissatisfaction triggers

### 9.2 Business Insight
Instead of a binary churn decision, risk-based segmentation enables prioritized and cost-effective retention strategies, focusing effort where it can deliver the highest impact.
________________________________________
## 10. Conclusion
In this project, machine learning techniques were applied to address customer churn challenges faced by No-Churn Telecom. An end-to-end pipeline was developed, including data extraction, exploratory data analysis, preprocessing, model training, and evaluation.
Exploratory analysis revealed that factors such as customer service calls, usage patterns, and service plans significantly influence churn behavior. Multiple classification models were evaluated using ROC-AUC, Recall, Precision, and F1-score to handle the inherent class imbalance in churn data.
Among the evaluated models, Random Forest demonstrated the best overall performance, achieving the highest ROC-AUC and F1-score while maintaining a balanced trade-off between identifying churn customers and minimizing false positives. Instead of relying on a fixed binary prediction, churn probabilities were converted into risk categories (Low, Medium, High) to enable actionable and cost-effective retention strategies.
This risk-based approach allows the business to prioritize customer retention efforts, optimize marketing campaigns, and proactively engage customers before churn occurs. The final solution is robust, interpretable, and suitable for real-world deployment.

