# DSC-PHASE-3-GROUP-2-
# 💉💉The Vaccine Uptake Prediction
## STEP 1: Business understanding
### Business Overview
A vaccine is a medical tool that helps the body build immunity against diseases. Vaccines not only protect individuals but also protect communities through herd immunity, where enough people are immunized to reduce the overall spread of disease.

There are different types of vaccines, such as the seasonal flu vaccine (for common flu strains) and the H1N1 vaccine (for swine flu). These play a key role in preventing large outbreaks and saving lives.

In 2009, the world faced a pandemic caused by the H1N1 influenza virus (swine flu), which led to an estimated 151,000–575,000 deaths globally in its first year. A vaccine for H1N1 was introduced in October 2009. Shortly after, the U.S. National 2009 H1N1 Flu Survey was conducted to measure who received the H1N1 and seasonal flu vaccines.

The survey also collected information on people’s demographics, health status, behaviors, and opinions. Studying this data helps us understand why some groups chose vaccination while others did not, and provides guidance for future public health efforts.

### Problem Statement
Although vaccines like the seasonal flu and H1N1 were available in 2009, uptake was low, especially for H1N1. This reflects vaccine hesitancy, which weakens herd immunity and increases disease risk.

The key challenge is to understand the factors influencing vaccination decisions—such as demographics, health beliefs, or doctor recommendations—and to build predictive models. These insights can help identify hesitant groups and support better public health strategies in future pandemics.

### Business Objectives
#### Main Objective
To build a predictive model that identifies the key factors influencing H1N1 flu vaccine uptake, to understand patterns of vaccine hesitancy, and provide insights that can guide future public health communication and decision-making.

#### Specific Objectives (NB// focused on H1N1 vaccine)
1.  To analyse the effect of demographic factors(i.e., age,education,income) on vaccine uptake.
2. To analyse the effect of opinions and beliefs (e.g., vaccine effectiveness, risk perceptions, safety concerns)on vaccine uptake.
3. To investigate the influence of health status and behaviours(e.g., chronic conditions, mask use, handwashing) in influencing vaccination uptake.
4. To investigate the influence of Doctor's recommendations and a health worker in influencing vaccination uptake.
#### Research Questions
1. How do demographic factors affect influence H1N1 vaccine uptake?
2. How do perceptions of vaccine effectiveness, risk of illness, and safety concerns affect H1N1 vaccination decisions uptake?
3. Do people with chronic medical conditions or protective behaviors (e.g., mask use, handwashing) show higher H1N1 vaccination uptake?
4. Does receiving a doctor’s recommendation or being a health worker increase the likelihood of getting the H1N1 vaccine?
#### Success Criteria
##### Business success criteria:
* Gain a clear understanding of H1N1 vaccine uptake patterns across different features.
* Identify key factors that influence vaccine decisions.
* Provide insights that can guide public health communication strategies to reduce vaccine hesitancy.
##### Data success criteria:
* Perform thorough EDA with at least 10 meaningful visualizations that answer the research questions.
* Build at least two classification models to predict H1N1 vaccine uptake.
* Identify and rank the most important features influencing H1N1 vaccination.
* Ensure results are interpretable and clearly communicated for both technical and non-technical audiences.

## STEP 2: Data Understanding

The dataset, sourced from the U.S. National 2009 H1N1 Flu Survey (H1N1_Flu_Vaccines.csv), contains 26,707 entries and 38 columns, covering:
1. Demographics: age_group, education, income_poverty, sex, race, marital_status, employment_status, etc.
2. Health Behaviors: behavioral_antiviral_meds, behavioral_face_mask, behavioral_wash_hands, etc.
3. Opinions and Beliefs: opinion_h1n1_vacc_effective, opinion_h1n1_risk, opinion_h1n1_sick_from_vacc, etc.
4. Health Status: chronic_med_condition, health_worker, health_insurance.
5. Target Variables: h1n1_vaccine (binary: 0 or 1), seasonal_vaccine.

### Key Dataset Details
* Shape: (26,707, 38)
* Data Types: 23 float64, 3 int64, 12 object.
* Missing Values: Notable in columns like health_insurance (14,433 non-null), employment_industry (13,377 non-null), and employment_occupation (13,237 non-null).
* Target Distribution: The h1n1_vaccine column is imbalanced, with significantly fewer positive cases (vaccinated), necessitating techniques like SMOTE for oversampling.

### Libraries Used
1. Data Manipulation: numpy, pandas
2. Visualization: matplotlib, seaborn
3. Modeling and Evaluation: scikit-learn (LogisticRegression, RandomForestClassifier, permutation_importance, RandomizedSearchCV), imblearn (SMOTE)
5. Gradient Boosting: Implied use of xgboost or similar for feature importance analysis.

## STEP 3: Data Preparation and Exploratory Data Analysis (EDA)
### Data Preparation
Handling Missing Values: Missing data was addressed through imputation (e.g., mode/median for categorical/numeric columns) or removal, depending on column importance and missingness percentage.
Feature Engineering: Categorical variables (e.g., age_group, education) were encoded (e.g., one-hot or ordinal encoding). Numeric features were scaled using StandardScaler.
Class Imbalance: The imbalanced h1n1_vaccine target was balanced using SMOTE to improve model performance.

### EDA Insights
Visualizations: Over 10 visualizations were created, including bar plots, heatmaps, and correlation matrices, to explore relationships between features and H1N1 vaccine uptake.
Below are some of the selected visualizations made from the project analysis:

* Bar plot to show how demographic factors affect H1N1 vaccination uptake
<img width="1984" height="1183" alt="image" src="https://github.com/user-attachments/assets/b0e572e2-fcec-4c3e-bd72-9cae2a27368c" />

* Correlation Heatmap: Behaviors and Conditions vs H1N1 Vaccine Uptake
<img width="1098" height="684" alt="image" src="https://github.com/user-attachments/assets/9bb64d11-04b7-41fe-b4d5-08ee8143b8b5" />

* Impact of Doctor Recommendation on H1N1 Vaccination and Impact of Health Worker Status on H1N1 Vaccination
<img width="1584" height="884" alt="image" src="https://github.com/user-attachments/assets/94ebbf51-9b71-4505-9e46-2db14aff8f38" />

* ROC curve using tuned random forest
<img width="784" height="584" alt="image" src="https://github.com/user-attachments/assets/e75b92e1-d8da-414b-ba53-0721d5e74813" />





### Key Findings:
1. Doctor Recommendations: Strong positive correlation with vaccine uptake, as individuals with a doctor’s recommendation were significantly more likely to get vaccinated.
2. Opinions and Beliefs: Higher perceived vaccine effectiveness (opinion_h1n1_vacc_effective) and perceived risk of H1N1 (opinion_h1n1_risk) were associated with increased uptake.
3. Health Behaviors: Protective behaviors like handwashing and mask-wearing showed moderate correlation with vaccination.
4. Demographics: Older age groups and higher education levels were linked to higher uptake, while income showed mixed effects.
5. Health Worker Status: Health workers were more likely to be vaccinated, likely due to greater exposure and awareness.

## STEP 4: Modelling
### Approach
Train-Test Split: The dataset was split into training and testing sets (e.g., 80/20 ratio) using train_test_split.
Models Built:
* Logistic Regression: A baseline model to capture linear relationships.
* Random Forest Classifier: An ensemble model to handle non-linear relationships and feature interactions.
* Gradient Boosting (e.g., via XGBoost): Used to assess feature importance and improve predictive performance.
* Hyperparameter Tuning: RandomizedSearchCV was used to optimize model parameters for better accuracy and generalization.

### Evaluation Metrics:
Accuracy, Precision, Recall, F1-Score, ROC-AUC, Confusion Matrix.
Emphasis on ROC-AUC due to class imbalance, ensuring effecient performance evaluation.

### Feature Importance
* Methodology: Permutation importance was computed using the Gradient Boosting model to rank features based on their impact on ROC-AUC.
* Top Features (from permutation importance):
1. doctor_recc_h1n1: Doctor’s recommendation was the strongest predictor.
2. opinion_h1n1_vacc_effective: Belief in vaccine effectiveness significantly influenced uptake.
3. opinion_h1n1_risk: Perceived risk of H1N1 infection was a key driver.
4. h1n1_knowledge: Higher knowledge about H1N1 increased vaccination likelihood.
5. health_worker: Health workers were more likely to be vaccinated.


## STEP 5: Evaluation and Results
### Model Performance
* Logistic Regression: Provided a baseline model with moderate performance, limited by its linear assumptions.
* Random Forest: Improved performance over Logistic Regression, capturing non-linear patterns.
* Gradient Boosting: Achieved the highest ROC-AUC, demonstrating robust predictive power due to its ability to handle complex feature interactions.
* Metrics: Specific performance metrics (e.g., ROC-AUC, F1-Score) were computed and detailed in the notebook, with 
Gradient Boosting outperforming others.

### Key Insights
1. Doctor Recommendations: The most influential factor, suggesting trusted medical advice is critical for vaccine uptake.
2. Perceptions Matter: Positive beliefs about vaccine effectiveness and H1N1 risk significantly drive vaccination decisions.
3. Knowledge and Awareness: Higher H1N1 knowledge correlates with increased uptake, highlighting the role of education.
4. Health Behaviors and Status: Chronic conditions and protective behaviors (e.g., mask-wearing) moderately increase uptake, likely due to heightened health awareness.
5. Demographics: Older age and higher education levels are associated with higher uptake, while income effects vary.

## STEP 6: Recommendations and Conclusions
### Recommendations
* Strengthen Doctor’s Role: Encourage healthcare providers to actively recommend the H1N1 vaccine, as their endorsement is the strongest predictor of uptake.
* Enhance Effectiveness Messaging: Develop campaigns that clearly communicate evidence of the vaccine’s effectiveness to build public trust.
* Increase Risk Awareness: Educate communities about the dangers of H1N1 infection to motivate vaccination.
* Address Knowledge Gaps: Target hesitant groups (e.g., low-knowledge or low-education populations) with clear, accessible educational materials.
* Leverage Health Workers: Use health workers as advocates to promote vaccination, given their higher uptake and influence.

### Conclusions
The project successfully identified key drivers of H1N1 vaccine uptake, with doctor recommendations, perceptions of vaccine effectiveness, and H1N1 risk being the most significant. The predictive models (especially Gradient Boosting) achieved strong performance, and the EDA provided clear insights into vaccine hesitancy patterns. These findings can guide public health officials in designing targeted interventions to boost vaccine uptake and strengthen herd immunity in future pandemics.

### PROJECT COLLABORATORS
1. Brian Kimathi(brian.kimathi1@student.moringaschool.com)
2. Sharon Wathiri(sharon.wathiri@student.moringaschool.com)
3. Zipporah Muriithi(zipporah.muriithi1@student.moringaschool.com)
4. Gabriel Tenesi(gabriel.tenesi@student.moringaschool.com)
5. Wesley Kipsang(wesley.kipsang@student.moringaschool.com)

### How to Run the Project
Clone the repository and Run the notebook: ([H1N1_vaccine_prediction.ipynb](https://github.com/Machinga1234/DSC-PHASE-3-GROUP-2-/blob/main/H1N1-prediction.ipynb) 


### Navigating the Repository
The repository contains:

*  Jupyter Notebook: ([H1N1_vaccine_prediction.ipynb](https://github.com/Machinga1234/DSC-PHASE-3-GROUP-2-/blob/main/H1N1-prediction.ipynb) (data analysis, modeling, visualizations)
* Presentation Slides: PDF file ( [The H1N1 Vaccine Uptake Prediction Presentation](https://github.com/Machinga1234/DSC-PHASE-3-GROUP-2-/blob/main/The%20H1N1%20Flu%20Vaccine%20Uptake%20Prediction%20Presentation%20(1).pdf)
* Dataset: ([H1N1_Flu_Vaccines.csv](https://github.com/Machinga1234/DSC-PHASE-3-GROUP-2-/blob/main/H1N1_Flu_Vaccines.csv)) (U.S. National 2009 H1N1 Flu Survey data)
* Data Report: ([Machine Learning Model to predict the uptake of H1N1](https://github.com/Machinga1234/DSC-PHASE-3-GROUP-2-/blob/main/Machine%20Learning%20Model%20to%20Predict%20the%20Uptake%20of%20H1N1-%20Data%20Report.docx) 
* README.md: Project overview 
* .gitignore: Specifies files to ignore in version control

