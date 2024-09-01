# Credit-Card-Financial-Dashboard-
The Credit Card Financial Dashboard offers a clear overview of credit card usage, tracking spending, balances, payment history, and credit utilization. It helps users monitor their financial health, identify spending patterns, and make informed decisions to manage their finances effectively and achieve their financial goals.

## Features
- **Interactive Dashboard**: Built using Power BI, the dashboard offers dynamic visualizations of transaction and customer data.
- **Data Processing & Analysis**: Optimized data handling ensures precise and efficient analysis.
- **Actionable Insights**: Provides critical insights that assist stakeholders in making strategic decisions.

## Data Sources
- **SQL Database**: The data is sourced from a SQL database containing detailed information on transactions and customers.

## Key Metrics
- Total Transactions
- Customer Demographics
- Spending Trends
- Credit Card Utilization

## DAX Queries

### Age Group Classification:
```DAX
AgeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[customer_age] < 30, "20-30",
    'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
    'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
    'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
    'public cust_detail'[customer_age] >= 60, "60+",
    "unknown"
)
```

### Income Group Classification:
```DAX
IncomeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[income] < 35000, "Low",
    'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] < 70000, "Med",
    'public cust_detail'[income] >= 70000, "High",
    "unknown"
)
```

### Week Number Calculation:
```DAX
week_num2 = WEEKNUM('public cc_detail'[week_start_date])
```

### Revenue Calculation:
```DAX
Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]
```

### Current Week Revenue Calculation:
```DAX
Current_week_Reveneue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
    )
)
```

### Previous Week Revenue Calculation:
```DAX
Previous_week_Reveneue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1
    )
)
```

## Project Insights

### Week-over-Week (WoW) Changes:
- **Revenue**: Increased by 28.8%
- **Total Transaction Amount & Count**: Increased by xx% & xx%
- **Customer Count**: Increased by xx%

### Year-to-Date (YTD) Summary:
- **Total Revenue**: $57M
- **Total Interest**: $8M
- **Total Transaction Amount**: $46M
- **Revenue by Gender**:
  - Male Customers: $31M
  - Female Customers: $26M
- **Credit Card Contributions**:
  - Blue & Silver Credit Cards: 93% of all transactions
- **Top Revenue-Generating States**: TX, NY, & CA contribute 68% of the total revenue
- **Activation Rate**: 57.5%
- **Delinquency Rate**: 6.06%


