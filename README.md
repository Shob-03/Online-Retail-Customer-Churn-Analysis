# 🛒 Online Retail Customer Churn Analysis — Power BI
Customer churn analysis for an online retail store built with Power BI — identifying churn rate, revenue loss and behavioural patterns across 1,000 customers

## 📌 Objective
Analyzed customer churn patterns for an online retail store to identify 
the churn rate, revenue lost, and key behavioural drivers behind 
customer attrition across 1,000 customers.

## 📂 Dataset
- **Source:** Kaggle — Online Retail Customer Churn Dataset
- **Records:** 1,000 customers
- **Tools Used:** Power BI, DAX
  
### Page 1 — Churn Overview
- Total Customers: 1,000 | Churned: 526 | Churn Rate: 52.60%
- Revenue Lost: $2.71M
- Churn rate breakdown by Age Group, Gender and Promotion Response
- Active vs Churned customer donut chart
- Churned customers by Satisfaction Score

### Page 2 — Churn Behaviour
- Avg Last Purchase Days Ago: 182.89
- Avg Satisfaction Score (Churned): 3.00
- Scatter plot — Purchases vs Spend colored by churn status
- Churn rate by Years as Customer
- Churn rate by Number of Support Contacts
- Last Purchase Days Ago comparison — Active vs Churned

## 🧮 DAX Measures & Calculated Columns

### Calculated Columns
```dax
-- Age Group segmentation
Age_Group = 
SWITCH(TRUE(),
    'online_retail_customer_churn'[Age] < 25, "18-24",
    'online_retail_customer_churn'[Age] < 35, "25-34",
    'online_retail_customer_churn'[Age] < 45, "35-44",
    'online_retail_customer_churn'[Age] < 55, "45-54",
    "55+"
)
```

### Measures
```dax
-- Churn Rate
Churn Rate = 
DIVIDE(
    CALCULATE(COUNTROWS('online_retail_customer_churn'),
    'online_retail_customer_churn'[Target_Churn] = TRUE()),
    COUNTROWS('online_retail_customer_churn')
) * 100

-- Churned Customers
Churned Customer = 
CALCULATE(COUNTROWS('online_retail_customer_churn'),
'online_retail_customer_churn'[Target_Churn] = TRUE())

-- Active Customers
Active Customer = 
CALCULATE(COUNTROWS('online_retail_customer_churn'),
'online_retail_customer_churn'[Target_Churn] = FALSE())

-- Revenue Lost to Churn
Revenue Lost = 
CALCULATE(SUM('online_retail_customer_churn'[Total_Spend]),
'online_retail_customer_churn'[Target_Churn] = TRUE())

-- Avg Satisfaction Score for Churned Customers
Avg Satisfaction (Churned) = 
CALCULATE(
    AVERAGE('online_retail_customer_churn'[Satisfaction_Score]),
    'online_retail_customer_churn'[Target_Churn] = TRUE()
)
```

## 🔍 Key Insights
- **52.6% of customers churned** resulting in $2.71M revenue lost
- **Churn is uniformly distributed across age, gender and promotion 
  response** — suggesting churn is driven by behavioural factors 
  rather than demographics
- **Customers aged 55+ have the highest churn rate** at 55%
- **Tenure does not significantly predict churn** — churn rate 
  fluctuates between 42-65% across all years as customer
- **Number of support contacts shows no clear churn pattern** — 
  churn rate stays between 51-54% regardless of contact frequency
- **Average last purchase days ago is similar** for both active 
  (184 days) and churned (181 days) customers suggesting 
  recency alone is not a strong churn predictor in this dataset

## 🛠️ Tools
- Power BI — dashboard and visualizations
- DAX — calculated measures and columns
