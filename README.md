# bank-churn-analysis
Pipeline to Identify and Retain At-Risk Customers
=====================================================================================================================================================



 Bank Customer Churn Prediction & Strategy
  Pipeline to Identify and Retain At-Risk Customers

Project Overview
    This project addresses a critical business problem in the financial sector:
    Customer Attrition. Using a dataset of 10,000 customers, I developed an end-to-end predictive pipeline that identifies high-risk individuals and provides actionable insights for retention strategies.


 1. Exploratory Data Analysis (EDA)
The analysis began by uncovering non-linear relationships between demographics and attrition.

Key Discoveries:
a.  The Age Factor       Churn risk peaks significantly in the 41-60 age bracket, suggesting a need for loyalty programs tailored to mid-life and senior demographics.
b.  The Product Paradox  Customers with 2 products show the lowest churn rates, while those with 3+ products are at extreme risk, indicating potential service friction.              c.  Engagement           Active membership is the strongest deterrent to churn, doubling the retention rate compared to inactive members.

---


 2. Feature Engineering & Preprocessing
To improve model performance, I engineered domain-specific features to capture complex behaviors:
Customer Personas: Categorical groups (e.g., "Ideal Customer," "Critically At Risk") based on the interaction between activity and product usage.
Financial Ratios: Balance per Product and Balance-to-Salary ratios to measure wealth density and "wallet share."
Lifecycle Features:Tenure-to-Age ratios to proxy long-term loyalty.

 Technical Implementation:
I used a Scikit-Learn `ColumnTransformer` to automate:
1.  Scaling: `StandardScaler` for all numerical and engineered ratios.
2.  Encoding: `OneHotEncoder` for categorical traits like Geography, Gender, and Life Stage.

---

3. Model Development & Optimization
I benchmarked three distinct algorithms to find the optimal balance of speed and precision.

| Model                         | Strategic Approach                    | Key Optimization |

| Logistic Regression**          | Linear Baseline                       | Tuned parameter for regularization. |
| Random Forest                  | Robust Ensemble                       | Balanced class weights to handle data imbalance. |
| XGBoost                        | Gradient Boosting                     | Dynamic `scale_pos_weight` to handle data imbalance. |

Hyperparameter Tuning:
Using `RandomizedSearchCV`, I optimized XGBoost over a wide parameter space (Learning Rate, Max Depth, Subsampling) to maximize the     ROC-AUC score.

---

 4. Strategic Evaluation
Instead of using a default 0.5 probability threshold, I implemented a 0.3 Threshold
In churn prediction, the cost of a "False Negative" (missing a churner) is much higher than a "False Positive" (sending a retention offer to a loyal customer).
This strategic shift significantly boosted Recall, ensuring the bank identifies up to 80-85% of actual churners.

---

5. Model Interpretability (SHAP)
 I utilized SHAP (SHapley Additive exPlanations).
The Age Gradient: Age remains a top global driver. The plot shows a clear transition: younger customers (blue) are pulled toward staying, while older customers (red) are pushed toward churning.
Product Intensity (NumOfProducts): This shows a clear "tipping point." High values (red) are pushed far to the right, indicating that as a customer holds more products beyond a certain threshold, their likelihood of exiting increases dramatically.

---
6. Business ROI: Decile Analysis
The model's value is finalized through Decile Analysis, which provides a "Retention Hit List."
Result:The Top 3 Deciles (highest 30% risk) contain over 60% of the total churn risk.
Action:The bank can achieve maximum impact by focusing marketing spend exclusively on these top three tiers, drastically reducing the cost-per-acquisition/retention.

==========================================================================================================================================================

