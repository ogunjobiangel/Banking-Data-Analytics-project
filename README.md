# 🏦 Banking Data Analytics Project

**Author:** Angel Ogunjobi | [@ogunjobiangel](https://github.com/ogunjobiangel)  
**Tools:** Python | SQL | Microsoft Excel | Power BI  
**Status:** Completed ✅

---

## Project Overview

This project analyses customer banking data to generate actionable insights on customer behaviour, transaction patterns, and financial performance. It demonstrates an end-to-end data analytics workflow — from raw data cleaning through to visual reporting — using industry-standard tools.

> *"This project analyzes customer banking data using Excel, SQL, Python, and Power BI to generate insights on customer behavior, transactions, and financial performance."*

---

## Business Questions Answered

| # | Question | Tool Used |
|---|----------|-----------|
| 1 | Which customer segments generate the most transaction volume? | SQL + Python |
| 2 | What are the peak transaction periods (day/month)? | Excel + Power BI |
| 3 | How do deposit and withdrawal trends compare month-on-month? | SQL + Excel |
| 4 | Which accounts show signs of high loan repayment risk? | SQL |
| 5 | What factors correlate most strongly with account balance growth? | Python (PCA, correlation) |

---

## Dataset

| Field | Description |
|---|---|
| `customer_id` | Unique customer identifier |
| `customer_name` | Customer full name |
| `account_type` | Savings / Current / Fixed Deposit |
| `segment` | Retail / SME / Corporate |
| `transaction_date` | Date of transaction |
| `transaction_type` | Deposit / Withdrawal / Transfer |
| `amount` | Transaction amount (₦) |
| `balance` | Account balance after transaction |
| `loan_status` | Active / Closed / Defaulted |

> **Note:** Dataset used is anonymised/simulated for portfolio purposes.

---

## Methodology

### Step 1 — Data Cleaning (Excel & Python)
- Removed duplicate transaction records
- Handled missing values in balance and loan fields
- Standardised date formats and transaction type labels
- Validated amount ranges (flagged negative balances)

### Step 2 — Exploratory Data Analysis (Python)
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv('bank_customers.csv')

# Transaction volume by segment
df.groupby('segment')['amount'].sum().sort_values(ascending=False).plot(
    kind='bar', color=['#003087', '#0066CC', '#3399FF'],
    figsize=(9, 5), edgecolor='black'
)
plt.title('Total Transaction Volume by Customer Segment')
plt.ylabel('Total Amount (₦ Millions)')
plt.xlabel('Customer Segment')
plt.tight_layout()
plt.savefig('outputs/segment_volume.png', dpi=150)
```

### Step 3 — SQL Analysis
```sql
-- Month-on-month transaction growth
SELECT 
    DATE_FORMAT(transaction_date, '%Y-%m') AS month,
    COUNT(*) AS transaction_count,
    SUM(amount) AS total_volume,
    LAG(SUM(amount)) OVER (ORDER BY DATE_FORMAT(transaction_date, '%Y-%m')) AS prev_month,
    ROUND(
        (SUM(amount) - LAG(SUM(amount)) OVER (ORDER BY DATE_FORMAT(transaction_date, '%Y-%m')))
        / LAG(SUM(amount)) OVER (ORDER BY DATE_FORMAT(transaction_date, '%Y-%m')) * 100, 2
    ) AS growth_pct
FROM transactions
GROUP BY month;
```

### Step 4 — Statistical Analysis (Python/R)
- Correlation matrix to identify relationships between balance, transaction frequency, and loan status
- Independent t-test comparing average balances between defaulted vs non-defaulted accounts
- PCA to identify key variables driving customer value

### Step 5 — Dashboard (Power BI / Excel)
Built interactive dashboard featuring:
- Monthly transaction trend line chart
- Customer segment breakdown (donut chart)
- Top 10 customers by balance (bar chart)
- Loan risk heatmap by region

---

## Key Insights

1. **Corporate segment** accounts for 54% of total transaction volume despite being only 12% of customers
2. **Monday and last-3-days-of-month** consistently show 35–40% higher transaction volumes — useful for staffing and liquidity planning
3. Accounts with **3+ missed loan payments** had average balances 62% lower than performing accounts — early warning signal for risk teams
4. PCA revealed that **transaction frequency and account tenure** explain 71% of variance in customer profitability

---

## Project Structure

```
Banking-Data-Analytics-Project/
│
├── data/
│   └── bank_customers_sample.csv
│
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_EDA.ipynb
│   └── 03_statistical_analysis.ipynb
│
├── sql/
│   └── banking_queries.sql
│
├── outputs/
│   ├── segment_volume.png
│   ├── monthly_trends.png
│   └── pca_plot.png
│
└── README.md
```

---

## How to Run

```bash
# Clone repository
git clone https://github.com/ogunjobiangel/Banking-Data-Analytics-Project.git

# Install dependencies
pip install pandas matplotlib seaborn scipy scikit-learn jupyter

# Launch notebooks
jupyter notebook
```

---

## About the Author

**Angel Ogunjobi** is a Microbiology graduate and NYSC corps member at the International Institute of Tropical Agriculture (IITA), with hands-on experience in statistical analysis (ANOVA, t-tests, PCA) using R and Python. Currently building expertise in data analytics with a focus on financial services.

📧 [ogunjobiangel2071@gmail.com]  
🔗 [LinkedIn](https://linkedin.com/in/your-profile)  
💻 [GitHub](https://github.com/ogunjobiangel)

---

*This project is part of my data analytics portfolio built in preparation for a career in financial services and banking.*
