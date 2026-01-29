# Customer Churning Prediction

A comprehensive machine learning project that predicts customer churn for a bank using various classification algorithms and hyperparameter optimization techniques.

## 📊 Dataset

The project uses the "Churn Modeling" dataset containing 10,000 customer records with the following features:

- **RowNumber**: Row index
- **CustomerId**: Unique customer identifier  
- **Surname**: Customer surname
- **CreditScore**: Customer's credit score
- **Geography**: Customer's country (France, Spain, Germany)
- **Gender**: Customer's gender (Male, Female)
- **Age**: Customer's age
- **Tenure**: Number of years with the bank
- **Balance**: Account balance
- **NumOfProducts**: Number of products owned
- **HasCrCard**: Has credit card (1/0)
- **IsActiveMember**: Active membership status (1/0)
- **EstimatedSalary**: Estimated salary
- **Exited**: Churn status (1=exited, 0=retained) - **Target Variable**

## 🛠️ Algorithms Used

### Primary Classification Algorithms
1. **Logistic Regression**
   - Linear classification algorithm
   - Test accuracy: 80.0%

2. **Naive Bayes Classifier (GaussianNB)**
   - Probabilistic classifier based on Bayes' theorem
   - Test accuracy: 79.15%

3. **Decision Tree Classifier**
   - Tree-based classification algorithm
   - Test accuracy: 100% (indicates overfitting)

4. **Random Forest Classifier**
   - Ensemble learning method with multiple decision trees
   - Base model test accuracy: 86.85%

5. **K-Nearest Neighbors (KNN)**
   - Instance-based learning algorithm
   - Test accuracy: 86.4%

6. **Support Vector Machine (SVM)**
   - Linear kernel SVM for classification
   - Test accuracy: 80.45%

7. **XGBoost Classifier**
   - Gradient boosting framework
   - Test accuracy: 86.7%

### Advanced Techniques
- **Hyperparameter Optimization**:
  - RandomizedSearchCV for Random Forest
  - GridSearchCV for fine-tuning
- **Cross-validation**: 5-fold and 10-fold CV
- **Feature Engineering**: Label encoding for categorical variables

## 📈 Model Performance

| Algorithm | Train Accuracy | Test Accuracy | ROC AUC Score |
|-----------|----------------|---------------|---------------|
| Logistic Regression | 78.8% | 80.0% | 0.520 |
| Naive Bayes | 78.19% | 79.15% | 0.523 |
| Decision Tree | 100% | 100% | 1.0 |
| Random Forest | 99.96% | 86.85% | 0.858 |
| KNN | 87.24% | 86.4% | 0.840 |
| SVM | 80.45% | 80.45% | 0.523 |
| XGBoost | 95.74% | 86.7% | 0.868 |

## 🔧 Implementation Details

### Data Preprocessing
- **Label Encoding**: Converted categorical variables (Geography, Gender) to numerical format
- **Feature Selection**: Removed irrelevant columns (RowNumber, CustomerId, Surname)
- **Train-Test Split**: 80% training, 20% testing

### Model Evaluation Metrics
- **Accuracy Score**: Overall prediction accuracy
- **ROC AUC Score**: Area under ROC curve for binary classification
- **Confusion Matrix**: True positive, false positive, true negative, false negative counts
- **Recall Score**: Ability to correctly identify positive cases

### Hyperparameter Tuning
The Random Forest model was extensively tuned using:
- **RandomizedSearchCV**: 100 iterations with 5-fold cross-validation
- **GridSearchCV**: Fine-tuned the best parameters with 10-fold cross-validation
- **Optimal Parameters**: 
  - criterion: 'entropy'
  - max_depth: 894
  - max_features: 'sqrt'
  - min_samples_split: 14

## 📁 Project Structure

```
Customer-Churning-Prediction/
├── Customer Churning Prediction.ipynb  # Main Jupyter notebook
├── Churn Modeling.csv                  # Dataset
└── README.md                           # This file
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

### Installation
```bash
pip install pandas numpy seaborn matplotlib scikit-learn xgboost jupyter
```

### Running the Analysis
1. Clone or download the repository
2. Navigate to the project directory
3. Start Jupyter Notebook:
   ```bash
   jupyter notebook
   ```
4. Open "Customer Churning Prediction.ipynb"
5. Run the cells sequentially

## 📊 Key Insights

- **Random Forest** and **XGBoost** performed best with ~87% test accuracy
- **Decision Tree** showed perfect accuracy but likely overfits the training data
- **Logistic Regression** and **SVM** provided baseline performance around 80%
- **Hyperparameter tuning** significantly improved Random Forest performance
- **Feature importance** analysis could provide insights into key churn drivers

## 🎯 Business Applications

This model can help banks:
- Identify customers at risk of churning
- Implement targeted retention strategies
- Optimize resource allocation for customer retention
- Reduce customer acquisition costs by improving retention rates

## 📝 Future Improvements

- **Feature Engineering**: Create additional features from existing data
- **Advanced Models**: Try neural networks, ensemble methods
- **Imbalanced Data Handling**: Use SMOTE or other techniques for class imbalance
- **Explainability**: Implement SHAP values for model interpretation
- **Real-time Prediction**: Deploy as an API for real-time churn prediction

## 📄 License

This project is open source and available under the MIT License.

