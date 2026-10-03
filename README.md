# 💼 Finance Dashboard — Power BI Project

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Data%20Modeling-blue)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

## 📊 Overview

This project analyzes customer–loan relationship data to extract key financial insights and support data-driven lending decisions. The dashboard identifies customer segments, loan performance patterns, and areas of financial risk across a portfolio of over 1,100 customers and $253M in loans.

The dashboard provides a comprehensive view of:
- Customer demographics and income distribution
- Loan portfolio performance across five loan types
- Default and high-risk loan trends
- Credit score behavior across gender, education, and employment status

---

## 🎯 Business Problem & Objective

A lending company needs visibility into who it's lending to and where its risk is concentrated, but that information is scattered across separate customer and loan records. Leadership needs to answer:

- Which customer segments carry the highest default and high-risk exposure?
- How does credit score vary across demographic and employment groups?
- Is the loan portfolio balanced across loan types, or overexposed to one category?
- Where should underwriting criteria be tightened to reduce future defaults?

The goal is to consolidate customer and loan data into a single model that supports credit risk management, loan approval strategy, and portfolio-level profitability decisions.

---

## 🧾 Dataset Description

### 1. Customer Details

| Column | Description |
|---|---|
| Customer ID | Unique identifier for each customer |
| Name | Customer name |
| Age | Customer age |
| Gender | Male / Female / Other |
| Income | Annual income of the customer |
| Employment Status | Full-time / Part-time / Self-employed / Unemployed |
| Educational Level | High School / Graduate / Postgraduate / Doctorate |
| Credit Score | Customer's credit rating |

### 2. Loan Details

| Column | Description |
|---|---|
| Loan ID | Unique loan identifier |
| Customer ID | Linked to Customer Details |
| Loan Amount | Total sanctioned amount |
| Interest Rate | Annual interest rate (%) |
| Term | Loan tenure (in months) |
| Loan Type | Student, Personal, Mortgage, Auto, or Small Business |
| Issue Date | Loan issue date |
| Status | Active / Closed / Defaulted |
| Monthly Installment | EMI amount |

---

## 🔗 Data Model & Integration

A dedicated **Date table** was built to support time-based analysis. Relationships:
- **Loan Details → Customer Details:** Many-to-One (`Customer_ID`)
- **Loan Details → Date Table:** Many-to-One (`Issue Date`)

This star-schema model enables slicing by time, customer attributes, and loan attributes simultaneously across all report pages.

---

## 🧮 KPI Development (Core DAX Measures)

```DAX
Default Rate % = 
DIVIDE([Defaulted Loan Amount], [Total Loan Amount], 0)

High Risk Exposure % = 
DIVIDE([High Risk Loan Amount], [Total Loan Amount], 0)

Total Customers = DISTINCTCOUNT(Customer_Details[Customer_ID])

---

## 📈 Dashboard Pages & Key Insights

1️⃣ Customer Demographics
KPIs: Total Customers, Average Income, Average Age

Portfolio Base: 1,155 total customers | $76.62K average income | 44.06 average age.

Credit Score Anomalies: Credit score does not scale linearly with education. High School-educated customers slightly outscore Postgraduates in the Male segment, suggesting credit health is driven more by historical repayment behavior/income than by educational attainment alone.

<img width="1331" height="746" alt="image" src="https://github.com/user-attachments/assets/3f9b8340-761f-4933-bcdb-7e9997fc0b2f" />


2️⃣ Loan Portfolio & Performance
KPIs: Total Loan Amount, Average Monthly Installment, Average Interest Rate

Diversification: The $253M portfolio is exceptionally well-diversified. Personal, Mortgage, Small Business, Auto, and Student loans each account for roughly 19%–20% of the total book, preventing heavy concentration risk in any single asset class.

Systemic Risk: All five loan types show a similar Active/Closed/Defaulted split, proving that default risk is a portfolio-wide issue rather than an isolated product failure.

Ticket Size: A significant skew toward large-ticket loans ($97K–$99K+) raises the financial stakes of the default rate

<img width="1252" height="740" alt="image" src="https://github.com/user-attachments/assets/72c80835-8d99-4561-89cd-e25168e0dee8" />


3️⃣ Financial Risk Analysis
KPIs: Default Rate (%), High-Risk Exposure (%), Defaulted Loan Amount, High-Risk Loan Amount

The Exposure Gap: The overall Default Rate sits at 10.35% ($26.19M), while High-Risk Exposure is an alarming 50.5% ($127.97M). The high-risk pipeline is roughly 5x larger than the defaulted pool, presenting a massive window for proactive intervention before these loans convert to bad debt.

The Employment Risk Myth: While Full-Time employees account for the highest raw volume of defaults, a cohort-level analysis reveals the actual Default Rate is distributed relatively evenly across employment types. This challenges legacy assumptions: full-time employment alone does not significantly insulate a loan from default.

Credit Score Density: Customer volume is heavily concentrated in the "Good" and "Very Good" credit bands, with far fewer customers in "Excellent." Because the portfolio sits heavily in this mid-tier risk zone, tightening underwriting criteria even slightly at the lower boundary of "Good" could drastically reduce the $127M high-risk exposure.

<img width="1337" height="745" alt="image" src="https://github.com/user-attachments/assets/0d0a1166-6db5-400e-8424-7cb3d93ec98e" />

4️⃣ Trend Analysis (Time Intelligence)KPIs: Origination Volume Trend, Default Rate TrendOrigination Trajectory: Loan originations experienced massive expansion between 2018 and 2020, reaching peak highs of $5.1M in early 2019. Moving into 2022–2024, origination volume has stabilized to a more consistent run rate, hovering between $2.6M and $4.4M per period.   Risk Cyclicality & Correlation: The default rate is highly volatile, experiencing severe spikes (peaking at a massive 21.85% in mid-2019) and sharp troughs (dropping to 0.92% in 2021). Crucially, the massive 21.85% default spike closely followed the portfolio's most aggressive $5.1M expansion period. This indicates that rapid scaling historically compromised underwriting quality.

<img width="1220" height="710" alt="image" src="https://github.com/user-attachments/assets/dc8179b7-64c3-4a70-8189-9ec9d1f23f27" />


---

💡 Strategic Recommendations
Shift Focus to Proactive Intervention: With $127M flagged as high-risk (5x the defaulted amount), the underwriting strategy must shift from purely reactive ("which segment do we avoid") to proactive ("how do we restructure high-risk loans before they default").

Tighten Mid-Tier Underwriting: Customer volume is heavily concentrated in the "Good" and "Very Good" credit bands. Tightening underwriting criteria even slightly at the lower boundary of "Good" could drastically reduce future high-risk exposure without suffocating overall loan volume.

Revamp Employment Weighting: Since Full-Time employment does not mathematically prevent defaults better than other statuses, the risk-scoring model should decrease the weight of employment type and increase the weight of historical repayment ratios.

Controlled Scaling: Historical trend analysis proves that rapid origination spikes directly preceded the worst default periods. Future growth initiatives must be paired with strict risk-tolerance caps to prevent a repeat of the 2019 default surge.

---
🔮 Future Improvements
Debt-to-Income (DTI) Analytics: Engineer a DTI ratio measure ([Monthly Installment] * 12 / [Income]) to identify the exact tipping point where loans become too expensive for customers to maintain.

"What-If" Scenario Modeling: Implement Power BI's What-If parameters to create a "Default Rate Stress Test" slider, allowing stakeholders to dynamically project financial losses under changing economic conditions.

Net Profitability Tracking: Calculate total expected interest revenue over the lifespan of active loans and compare it against the defaulted loan amount to track true unit economics (Revenue vs. Risk).

## 🧠 Skills Demonstrated

`Data Modeling` · `DAX` · `Power Query (ETL)` · `Star-Schema Design` · `Credit Risk Analysis` · `Customer Segmentation` · `KPI Design` · `Dashboard/UX Design`

---

🛠️ Tech Stack & Skills Demonstrated
Tools: Power BI Desktop, Power Query, Excel / CSV

Skills: Time Intelligence Analytics, Relational Data Modeling, DAX, Credit Risk Analysis, Portfolio Segmentation, Executive Dashboard Design

---

## 📁 Repository Structure

```
Finance-Dashboard/
│
├── Financial_Dashboard.pbix      # Power BI report file
├── Finance_DATA.xlsx             # Source data
├── README.md                     # Project documentation (this file)
└── images/
    ├── customer_demographics.png
    ├── loan_portfolio_performance.png
    └── financial_risk_analysis.png
```
---



## 👤 Author

**Karan Kumar Sahu**
Data Analyst | SQL · Python · Power BI
