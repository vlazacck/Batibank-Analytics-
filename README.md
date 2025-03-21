# Bati Bank Analytics - Credit Scoring Model

## Overview
### Business Need
Bati Bank, a leading financial service provider with over 10 years of experience, is partnering with a rapidly growing eCommerce company to enable a buy-now-pay-later (BNPL) service. This service allows customers to purchase products on credit if they qualify.

To support this initiative, Bati Bank requires a Credit Scoring Model that evaluates a customer's creditworthiness based on transaction data. The goal is to assess default risk and optimize loan offerings.

## Project Objectives
The project aims to develop a Credit Scoring Model that:
- Defines a proxy variable for categorizing users as high risk (bad) or low risk (good).
- Selects observable features that strongly predict default risk.
- Develops a model that assigns a risk probability to new customers.
- Builds a credit scoring system based on risk probability estimates.
- Predicts the optimal loan amount and duration for a customer.

## Data and Features
The dataset is sourced from the Xente Challenge on Kaggle and contains customer transaction information. Key fields include:

### Transaction Details:
- `TransactionId`: Unique identifier for each transaction.
- `BatchId`: Identifier for batches of transactions.
- `TransactionStartTime`: Timestamp of the transaction.
- `Amount`: Transaction value (positive for debits, negative for credits).
- `Value`: Absolute value of the transaction.

### Customer and Account Information:
- `AccountId`: Unique customer account number.
- `SubscriptionId`: Subscription identifier.
- `CustomerId`: Unique identifier for a customer.

### Product and Merchant Details:
- `ProductId`: Name of the purchased product.
- `ProductCategory`: Broad category of the product.
- `ProviderId`: Source provider of the purchased item.

### Channel and Currency Information:
- `ChannelId`: Identifies if the transaction was via web, Android, iOS, Pay Later, or Checkout.
- `CurrencyCode`: Currency of the transaction.
- `CountryCode`: Geographical code of the country.

### Fraud Detection:
- `FraudResult`: Indicates if the transaction was fraudulent (1 - Yes, 0 - No).

## Methodology
The project follows a structured approach:

### 1. Data Preprocessing & Feature Engineering
#### Handling Missing Data:
- Imputed missing values using statistical methods.

#### Feature Engineering:
- **Transaction Aggregation:**
  - Total, average, and standard deviation of transaction amounts.
  - Count of transactions per user.
- **Time-Based Features:**
  - Extracted transaction hour, day, month, and year.
- **Categorical Encoding:**
  - One-hot encoding for categorical variables.
  - Label encoding where applicable.
- **Scaling:**
  - Normalized and standardized numerical features for model compatibility.

### 2. Credit Risk Modeling
#### Defining a Default Proxy Variable:
- Applied RFMS (Recency, Frequency, Monetary, Stability) analysis to classify users into high-risk (bad) and low-risk (good) categories.
- Used customer transaction history to determine the likelihood of default.

#### Feature Selection:
- Used correlation analysis and Weight of Evidence (WoE) binning to select the most predictive features.

#### Model Training:
- Trained Random Forest and Logistic Regression models for risk classification.
- Optimized models using hyperparameter tuning.
- Evaluated models using Accuracy, Precision, Recall, F1 Score, and ROC-AUC.

### 3. Credit Scoring & Loan Prediction
#### Risk Probability Estimation:
- Assigned a risk score based on model predictions.
- Higher probability indicated a higher likelihood of default.

#### Credit Score Calculation:
- Transformed risk probabilities into a standardized credit score.

#### Loan Amount and Duration Prediction:
- Developed an estimator to predict optimal loan terms based on customer risk profile.

### 4. Model Deployment
#### API Development:
- Built a REST API using FastAPI to serve the credit scoring model.
- Endpoints:
  - `/predict` - Accepts customer data and returns risk probability.
  - `/score` - Returns a credit score based on model predictions.
  - `/loan` - Suggests an optimal loan amount and duration.

#### Deployment Strategy:
- Containerized the API using Docker.
- Cloud deployment planned but pending infrastructure setup.

## Results & Insights
- RFMS Analysis successfully segmented customers into high and low-risk groups.
- Random Forest Model outperformed Logistic Regression, achieving better precision and recall.
- Feature Engineering improved model interpretability and predictive power.
- Loan Estimator provided tailored loan recommendations based on credit scores.

## Next Steps
- Deploy the model on a cloud platform for real-time credit scoring.
- Implement a monitoring system to track model performance.
- Expand the feature set using external credit bureau data for improved risk assessment.

## Project Structure
```
├── src/                # Core scripts for data processing and modeling
│   ├── data_preprocessing.py
│   ├── feature_engineering.py
│   ├── model_training.py
│   ├── credit_scoring.py
│   ├── loan_prediction.py
│   ├── api.py          # FastAPI implementation
│   ├── utils.py
│
├── notebooks/          # Jupyter notebooks for EDA and model experiments
│
├── data/               # Raw and processed datasets
│   ├── raw/
│   ├── processed/
│
├── tests/              # Unit tests for core functions
│
├── scripts/            # Utility scripts for automation
│
├── docker/             # Docker setup for deployment
│
├── README.md           # Project documentation
├── requirements.txt    # Dependencies list
├── config.yaml         # Configuration settings
└── .gitignore          # Files to ignore in version control
```

## How to Run

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/bati-bank-analytics.git
cd bati-bank-analytics
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the API Locally
```bash
uvicorn src.api:app --reload
```
Access the API documentation at: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

### 4. Run Tests
```bash
pytest tests/
```

## Contributors
- **Mikias**

