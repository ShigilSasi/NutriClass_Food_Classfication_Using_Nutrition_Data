# NutriClass_Food_Classfication_Using_Nutrition_Data

## Project Overview

NutriClass is a machine learning project that predicts the food category (Pizza, Burger, Apple, Sushi, etc.) using nutritional values and dietary attributes.
The goal is to demonstrate data preprocessing, statistical analysis, feature engineering, and multi-model classification on a real-world-like dataset.

## Dataset Information

Total records (before cleaning): 31,700
After removing duplicates: 31,387
Features: 15
Target: Food_Name (10 classes)

## Feature Types
| Type        | Features                                                                                                      |
| ----------- | ------------------------------------------------------------------------------------------------------------- |
| Numerical   | Calories, Protein, Fat, Carbs, Sugar, Fiber, Sodium, Cholesterol, Glycemic_Index, Water_Content, Serving_Size |
| Categorical | Meal_Type, Preparation_Method                                                                                 |
| Binary      | Is_Vegan, Is_Gluten_Free                                                                                      |
| Target      | Food_Name                                                                                                     |


## Data Cleaning
Duplicate Handling
313 duplicate rows were removed to prevent model bias.

Missing Values
127 values were missing in all numerical nutrition columns.

Why Median Imputation?
Skewness analysis showed high right-skewed distributions:

| Feature       | Skewness |
| ------------- | -------- |
| Water_Content | 4.15     |
| Cholesterol   | 3.65     |
| Fiber         | 3.61     |
| Protein       | 3.09     |
| Sugar         | 2.81     |

## Hypothesis Testing
Categorical vs Target (Chi-Square Test)
Meal_Type and Preparation_Method were dropped due to lack of statistical relationship with Food_Name
Is_Vegan and Is_Gluten_Free were identified as leakage features that strongly encode the target and were excluded for fair modeling

Numerical vs Target (ANOVA)
ANOVA tests showed:
Calories, Protein, Fat, Sugar, Sodium, etc. all had p-value < 0.05
Therefore, they significantly influence food classification
No important feature was removed.

## Preprocessing Pipeline
| Step                   | Method              |
| ---------------------- | ------------------- |
| Missing numeric values | Mean Imputation     |
| Scaling                | StandardScaler      |
| Boolean to Int         | True → 1, False → 0 |
| Categorical Imputation | Most Frequent       |
| Column-wise handling   | ColumnTransformer   |

## Models Trained
The following models were trained and evaluated:
Logistic Regression
Decision Tree
Random Forest
KNN
SVC
Gradient Boosting
XGBoost
All models used the same preprocessing pipeline for fair comparison.

## Model Performance (Test Set)
| Model                 | Accuracy |
| --------------------- | -------- |
| Logistic Regression   | 99%      |
| Decision Tree         | 99%      |
| Random Forest         | 99%      |
| Random Forest (Tuned) | 99%      |
| SVC                   | 99%      |
| KNN                   | 99%      |
| Gradient Boosting     | 99%      |
| XGBoost               | 99%      |

Random Forest Hyperparameter Tuning
GridSearchCV was used to optimize Random Forest:
Best Parameters
n_estimators = 15  
max_depth = 10  
min_samples_split = 5  
min_samples_leaf = 4  
criterion = entropy

## Conclusion
This project demonstrates a complete ML pipeline:
Data Cleaning
Statistical Validation
Feature Engineering
Model Training
Hyperparameter Tuning
Final Evaluation
The system can accurately classify food types using nutritional information, which can be useful for:
Diet tracking apps
Health analytics
Food recommendation systems