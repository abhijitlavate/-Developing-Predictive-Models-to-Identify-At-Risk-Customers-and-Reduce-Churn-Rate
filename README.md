# -Developing-Predictive-Models-to-Identify-At-Risk-Customers-and-Reduce-Churn-Rate
# 📊 Project: Developing Predictive Models to Identify At-Risk Customers and Reduce Churn Rate

## 🧠 Problem Statement

As a Data Analyst, this project explores extensive datasets from banking and telecom sectors to analyze customer churn. By leveraging customer features like demographics, transaction history, and activity status, the goal is to develop predictive models to forecast churn, generate actionable insights, and empower businesses to retain valuable customers.

---

## 📌 Key Features

### 🔐 Customer Information
- **RowNumber**: Unique row ID  
- **CustomerId**: Customer unique ID  
- **CreditScore**: Customer credit score  
- **GeographyID**: Location reference  
- **GenderID**: Gender reference  
- **Age**: Customer age  
- **Tenure**: Years with the company  
- **Balance**: Account balance  
- **NumOfProducts**: Number of subscribed products  
- **HasCrCard**: Credit card holder flag  
- **IsActiveMember**: Activity status flag  
- **EstimatedSalary**: Salary estimate  
- **Exited**: Churn indicator  
- **Bank DOJ**: Bank joining date  

### 🌍 Geography Table
- **GeographyID**  
- **GeographyLocation**

### 👤 Gender Table
- **GenderID**  
- **GenderCategory**

### ❌ Customer Exit Table
- **ExitID**  
- **ExitCategory**

### 💳 Credit Card Table
- **CreditID**  
- **Category**

### 🔄 Active Customers Table
- **ActiveID**  
- **ActiveCategory**

---

## 🎯 Analysis Objectives

### 🔍 Identifying Key Churn Drivers
- Analyze churn contributors across banking and telecom sectors  
- Evaluate customer attributes vs. churn correlation  
- Detect patterns separating retained vs. churned customers  

### 🧩 Customer Segmentation
- Cluster customers by demographics, transactions & activity  
- Compare churn rates across different segments  
- Identify high-value but churn-prone segments  

### 🤖 Predictive Modeling
- Build ML models to forecast customer churn  
- Evaluate model accuracy and feature importance  
- Deploy best-performing model for business use  

### 💰 Customer Lifetime Value (CLV)
- Calculate CLV for various segments  
- Analyze how churn affects CLV  
- Recommend strategies to increase CLV & reduce churn  

### 🔁 Retention Strategy Recommendations
- Offer insights for churn prevention  
- Design targeted retention campaigns  
- Simulate strategies using A/B testing  

### 📈 Continuous Monitoring & Improvement
- Create feedback loops for model optimization  
- Monitor real-time churn & adjust strategies  
- Track KPIs and retention performance over time  

---

## 🧮 DAX Measures Implementation

```DAX
-- Active Members
ActiveMembers = CALCULATE(COUNT(Bank_Churn[CustomerId]), 'Active customers'[ActiveCategory] = "Active member")

-- Churn Percentage
Churn% = 
VAR EC = [Exit Customers]
VAR TC = [Total Customers]
RETURN DIVIDE(EC, TC)

-- Credit Card Holders
Credit Card Holders = CALCULATE(COUNT(Bank_Churn[CustomerId]), 'Credit card'[Category] = "credit card holder")

-- Exit Customers
Exit Customers = CALCULATE(COUNT(CustomerInfo[CustomerId]), 'Customer Exit'[ExitCategory] = "Exit")

-- Inactive Members
Inactive members = CALCULATE(COUNT(Bank_Churn[CustomerId]), 'Active customers'[ActiveCategory] = "Inactive Member")

-- Non Credit Card Holders
Non credit card holders = CALCULATE(COUNT(Bank_Churn[CustomerId]), 'Credit card'[Category] = "non credit card holder")

-- Previous Month Exit Customers
Previous month exit customers = CALCULATE([Exit Customers], PREVIOUSMONTH('Date Master'[Date]))

-- Retain Customers
Retain customers = [Total Customers] - [Exit Customers]

-- Total Customers
Total Customers = COUNT(Bank_Churn[CustomerId])
