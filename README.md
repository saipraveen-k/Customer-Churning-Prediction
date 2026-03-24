

# Customer Churning Prediction

A comprehensive machine learning project that predicts customer churn for a bank using various classification algorithms, clustering techniques, and advanced hyperparameter optimization methods.

## 📊 Dataset Overview

The project uses the "Churn Modeling" dataset containing **10,000 customer records** with **14 features**:

### Features Description
- **RowNumber**: Row index (removed during preprocessing)
- **CustomerId**: Unique customer identifier (removed during preprocessing)
- **Surname**: Customer surname (removed during preprocessing)
- **CreditScore**: Customer's credit score (350-850)
- **Geography**: Customer's country (France, Spain, Germany) - Label encoded
- **Gender**: Customer's gender (Male, Female) - Label encoded
- **Age**: Customer's age (18-92 years)
- **Tenure**: Number of years with the bank (0-10 years)
- **Balance**: Account balance ($0 - $250,898)
- **NumOfProducts**: Number of products owned (1-4)
- **HasCrCard**: Has credit card (0/1)
- **IsActiveMember**: Active membership status (0/1)
- **EstimatedSalary**: Estimated salary ($11.58 - $199,992)
- **Exited**: Churn status (1=exited, 0=retained) - **Target Variable**

### Class Distribution
- **Non-churned (0)**: 7,963 customers (79.63%)
- **Churned (1)**: 2,037 customers (20.37%)
- **Imbalance Ratio**: ~4:1 (moderate imbalance)

## 🛠️ Methodologies and Algorithms Used

### 1. Data Preprocessing
- **Label Encoding**: Converted categorical variables (Geography, Gender) to numerical format
- **Feature Selection**: Removed irrelevant columns (RowNumber, CustomerId, Surname)
- **Train-Test Split**: 80% training (8,000 samples), 20% testing (2,000 samples)

### 2. Exploratory Data Analysis
- **Statistical Analysis**: Descriptive statistics, data type analysis, missing value detection
- **Data Visualization**: 15+ bar plots and pair plots showing relationships between features
- **Distribution Analysis**: Histograms for all numerical features to check skewness

### 3. Association Rule Mining (Apriori Algorithm)
- **Purpose**: Discover interesting relationships between customer attributes
- **Implementation**: Used mlxtend library with TransactionEncoder
- **Parameters**: min_support=0.05, min_confidence=0.6
- **Output**: 166 association rules with support, confidence, and lift metrics

### 4. Customer Segmentation (K-Means Clustering)
- **Features Used**: CreditScore, Age, Balance
- **Clusters**: 3 customer segments
- **Purpose**: Identify natural customer groupings for targeted marketing

### 5. Classification Algorithms

#### Primary Models
1. **Logistic Regression**
   - Linear classification algorithm
   - Train Accuracy: 79.24%
   - Test Accuracy: 79.95%
   - ROC AUC: 0.571
   - Kappa Score: 0.181

2. **Naive Bayes Classifier (GaussianNB)**
   - Probabilistic classifier based on Bayes' theorem
   - Train Accuracy: 78.19%
   - Test Accuracy: 79.15%
   - ROC AUC: 0.523
   - Kappa Score: 0.063

3. **Decision Tree Classifier**
   - Tree-based classification algorithm
   - Train Accuracy: 100%
   - Test Accuracy: 100%
   - ROC AUC: 1.0
   - Kappa Score: 1.0
   - **Issue**: Severe overfitting detected

4. **Random Forest Classifier**
   - Ensemble learning method with multiple decision trees
   - Base Model:
     - Train Accuracy: 99.99%
     - Test Accuracy: 87.65%
     - ROC AUC: 0.739
     - Kappa Score: 0.546

5. **K-Nearest Neighbors (KNN)**
   - Instance-based learning algorithm
   - Train Accuracy: 81.05%
   - Test Accuracy: 77.05%
   - ROC AUC: 0.509
   - Kappa Score: 0.023

6. **Support Vector Machine (SVM)**
   - Linear kernel SVM for classification
   - Train Accuracy: 79.89%
   - Test Accuracy: 79.45%
   - ROC AUC: 0.516
   - Kappa Score: 0.159

7. **XGBoost Classifier**
   - Gradient boosting framework
   - Train Accuracy: 95.74%
   - Test Accuracy: 86.70%
   - ROC AUC: 0.868
   - Kappa Score: 0.531

### 6. Hyperparameter Optimization

#### RandomizedSearchCV
- **Algorithm**: Random Forest Classifier
- **Iterations**: 100
- **Cross-validation**: 5-fold
- **Best Parameters**:
  - criterion: 'entropy'
  - max_depth: 894
  - max_features: 'sqrt'
  - min_samples_leaf: 1
  - min_samples_split: 14
  - n_estimators: 1556
- **Test Accuracy**: 87.85%
- **Wrong Predictions**: 243/2000

#### GridSearchCV
- **Algorithm**: Random Forest Classifier
- **Cross-validation**: 10-fold
- **Parameters**: Fine-tuned around RandomizedSearchCV results
- **Best Parameters**:
  - criterion: 'entropy'
  - max_depth: 894
  - max_features: 'sqrt'
  - min_samples_split: 14
- **Test Accuracy**: 87.70%
- **Wrong Predictions**: 246/2000

## 📈 Performance Comparison

| Algorithm | Train Accuracy | Test Accuracy | ROC AUC | Kappa Score | Status |
|-----------|----------------|---------------|---------|-------------|---------|
| Logistic Regression | 79.24% | 79.95% | 0.571 | 0.181 | Baseline |
| Naive Bayes | 78.19% | 79.15% | 0.523 | 0.063 | Poor |
| Decision Tree | 100% | 100% | 1.0 | 1.0 | Overfitted |
| Random Forest | 99.99% | 87.65% | 0.739 | 0.546 | Good |
| KNN | 81.05% | 77.05% | 0.509 | 0.023 | Poor |
| SVM | 79.89% | 79.45% | 0.516 | 0.159 | Baseline |
| XGBoost | 95.74% | 86.70% | 0.868 | 0.531 | Good |
| **Random Forest (Tuned)** | - | **87.85%** | - | - | **Best** |

## 🔧 Technical Implementation

### Libraries Used
```python
# Data Manipulation
import pandas as pd
import numpy as np

# Visualization
import seaborn as sns
import matplotlib.pyplot as plt

# Machine Learning
from sklearn.preprocessing import LabelEncoder
from sklearn.model_selection import train_test_split, RandomizedSearchCV, GridSearchCV
from sklearn.linear_model import LogisticRegression
from sklearn.naive_bayes import GaussianNB
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
from sklearn.neighbors import KNeighborsClassifier
from sklearn.svm import SVC
from sklearn.cluster import KMeans
import xgboost as xgb

# Association Rules
from mlxtend.frequent_patterns import apriori, association_rules
from mlxtend.preprocessing import TransactionEncoder

# Metrics
from sklearn.metrics import (accuracy_score, confusion_matrix, roc_auc_score, 
                           roc_curve, recall_score)
from sklearn import metrics
```

### Data Preprocessing Pipeline
1. **Load Data**: Read CSV dataset
2. **Initial Analysis**: Shape, info, missing values, descriptive statistics
3. **Label Encoding**: Convert Geography and Gender to numerical
4. **Feature Selection**: Drop unnecessary columns
5. **Train-Test Split**: 80-20 split with random_state=40

### Model Evaluation Metrics
- **Accuracy Score**: Overall prediction accuracy
- **ROC AUC Score**: Area under ROC curve for binary classification
- **Confusion Matrix**: TP, FP, TN, FN counts
- **Kappa Score**: Inter-rater agreement measure
- **Recall Score**: True positive rate

## 📁 Project Structure

```
Customer-Churning-Prediction/
├── Customer Churning Prediction.ipynb  # Complete analysis notebook
├── Churn Modeling.csv                  # Dataset (10,000 records)
└── README.md                           # This documentation
```

## 🚀 Getting Started

### Prerequisites
- Python 3.7+
- Jupyter Notebook
- Required libraries:
  - pandas
  - numpy
  - seaborn
  - matplotlib
  - scikit-learn
  - xgboost
  - mlxtend

### Installation
```bash
pip install pandas numpy seaborn matplotlib scikit-learn xgboost mlxtend jupyter
```

### Running the Analysis
1. Clone or download the repository
2. Navigate to the project directory
3. Start Jupyter Notebook:
   ```bash
   jupyter notebook
   ```
4. Open "Customer Churning Prediction.ipynb"
5. Run cells sequentially (81 cells total)

## 📊 Key Findings and Insights

### Model Performance Insights
- **Random Forest** and **XGBoost** performed best with ~87% test accuracy
- **Decision Tree** showed perfect accuracy but severely overfit
- **Logistic Regression** and **SVM** provided baseline performance around 80%
- **Hyperparameter tuning** marginally improved Random Forest performance
- **KNN** and **Naive Bayes** performed poorly on this dataset

### Business Insights
- **Customer Segmentation**: K-means identified 3 distinct customer groups
- **Association Rules**: Found 166 significant relationships between customer attributes
- **Churn Rate**: 20.37% overall churn rate indicates moderate customer retention issues
- **Feature Importance**: Age, Balance, and CreditScore were key clustering features

## 🎯 Business Applications

This model can help banks:
- **Predictive Analytics**: Identify customers at risk of churning with 87.85% accuracy
- **Customer Segmentation**: Target specific customer segments with personalized offers
- **Resource Optimization**: Focus retention efforts on high-risk customers
- **Cost Reduction**: Reduce customer acquisition costs through improved retention
- **Strategic Planning**: Use association rules for cross-selling and upselling strategies

## 📝 Limitations and Future Improvements

### Current Limitations
- **Class Imbalance**: Moderate imbalance (4:1) not addressed with sampling techniques
- **Overfitting**: Decision Tree shows severe overfitting
- **Feature Engineering**: Limited feature engineering performed
- **Model Interpretability**: Lack of SHAP values or feature importance analysis

### Future Improvements
- **Imbalanced Data Handling**: Implement SMOTE, ADASYN, or class weighting
- **Advanced Feature Engineering**: Create interaction terms, polynomial features
- **Neural Networks**: Try deep learning approaches
- **Ensemble Methods**: Stacking or blending multiple models
- **Explainability**: Implement SHAP values for model interpretation
- **Cross-validation**: Use stratified k-fold for more robust evaluation
- **Real-time Deployment**: Create API for production use

## 📄 License

This project is open source and available under the MIT License.
