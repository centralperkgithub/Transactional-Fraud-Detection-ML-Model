
# **💸 Financial Transaction Fraud Detection Model 💸**

<img width="1534" height="155" alt="image" src="https://github.com/user-attachments/assets/be8f14d5-a44c-4c77-a79d-13c3cb0b3f9d" />

---

## 📑 Table of Contents
1. [Project Overview](#project-overview)  
2. [Key Features & Objectives](#-key-features--objectives)  
3. [Dataset Overview](#-dataset-overview)  
4. [Data Cleaning & Preprocessing](#-data-cleaning--preprocessing)  
5. [Exploratory Data Analysis (EDA)](#-exploratory-data-analysis-eda---key-insights)  
6. [Feature Engineering](#️-feature-engineering)  
7. [Model Development & Evaluation](#-model-development--evaluation-logistic-regression)  
8. [Key Predictive Factors](#-key-predictive-factors--real-world-relevance)  
9. [Business Recommendations](#-business-recommendations-for-infrastructure-updates)  
10. [Validation & Monitoring](#-validation--monitoring-of-recommendations)  
11. [Technologies Used](#-technologies-used)  
12. [Future Enhancements](#-future-enhancements)  
13. [How to Run Locally](#-how-to-run-the-project-locally)  
14. [Contact](#-contact)  

---

## 📌 Project Overview
This project builds a **machine learning model** to detect fraudulent financial transactions.  
Fraud leads to **monetary loss, reputational damage, and loss of customer trust**.  
By combining **data analysis, feature engineering, and ML modeling**, the project uncovers fraud patterns and proposes **business recommendations** to strengthen financial infrastructure.  

Dataset: `Fraud.csv` (6.3M+ records)  
Notebook: `Transaction Fraud Detection Model.ipynb`  

---

## 🚀 Key Features & Objectives
- **Proactive Fraud Detection** – Catch fraudulent activity before losses occur  
- **Data-Driven Insights** – Understand hidden fraud behavior patterns  
- **ML Implementation** – Train & evaluate classification models  
- **Robust Evaluation** – Use metrics suitable for imbalanced datasets  
- **Business Recommendations** – Suggest real-world fraud prevention steps  

---

## 📊 Dataset Overview
Dataset: `Fraud.csv` (30 days of transactions, 744 hourly steps, 11 attributes).  

**Attributes:**  
- `step`: Transaction time step (1 step = 1 hour, total 744 steps)  
- `type`: Transaction type (CASH-IN, CASH-OUT, DEBIT, PAYMENT, TRANSFER)  
- `amount`: Transaction amount  
- `nameOrig`: Customer initiating transaction  
- `oldbalanceOrg`, `newbalanceOrig`: Origin account balances before & after  
- `nameDest`: Recipient account  
- `oldbalanceDest`, `newbalanceDest`: Destination balances before & after  
- `isFraud`: **Target variable** (1 = Fraud, 0 = Genuine)  
- `isFlaggedFraud`: Transactions flagged by rule (`amount > 200k`)  

---

## 🧹 Data Cleaning & Preprocessing
- **Missing Values:** None (0 balances for merchants are valid, not missing)  
- **Outliers:** Extreme transaction amounts retained (key fraud signals)  
- **Multicollinearity:** Detected between old/new balances; engineered difference features instead of removal  

---

## 🔎 Exploratory Data Analysis (EDA) – Key Insights
- **Severe Class Imbalance:** Only **0.13% transactions are fraud**  
- **Fraud occurs only in:** `TRANSFER` & `CASH_OUT` types  
- **Large Amounts → Higher Fraud Probability**  
- **Balance Inconsistencies:**  
  - Account draining (`oldbalanceOrg > 0` & `newbalanceOrig = 0`) → strong fraud indicator  
- **isFlaggedFraud Ineffective:** Flagged only 16 cases, despite high precision  

---

## ⚙️ Feature Engineering
New engineered features:  
- `balanceDiffOrig = oldbalanceOrg - newbalanceOrig`  
- `balanceDiffDest = newbalanceDest - oldbalanceDest`  
- Account draining flags  

Dropped: `step`, `nameOrig`, `nameDest`, `isFlaggedFraud`  

---

## 🤖 Model Development & Evaluation (Logistic Regression)
**Pipeline:**  
- `StandardScaler` → Numerical features  
- `OneHotEncoder` → Transaction type  
- Logistic Regression with `class_weight=balanced`  

### ✅ Performance Results
**Classification Report:**  
- Accuracy: **95%**  
- Fraud Recall: **0.95** (excellent detection rate)  
- Fraud Precision: **0.02** (many false positives)  
- ROC-AUC: **0.99**  
- PR-AUC: **0.72**  

---
```
