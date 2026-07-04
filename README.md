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

## 🧮 KPI Development (DAX Measures)

| KPI | DAX Formula |
|---|---|
| Average Age | `AVERAGE(Customer_Details[Age])` |
| Average Income | `AVERAGE(Customer_Details[Income])` |
| Average Interest Rate | `AVERAGE(Loan_Details[Interest_Rate])` |
| Average Monthly Installment | `AVERAGE(Loan_Details[Monthly_Installment])` |
| Total Customers | `COUNTA(Customer_Details[Customer_ID])` |
| Total Loan Amount | `SUM(Loan_Details[Loan_Amount])` |
| Defaulted Loan Amount | `CALCULATE(SUM(Loan_Details[Loan_Amount]), FILTER(Loan_Details, Loan_Details[Status] = "Defaulted"))` |
| Defaulted Loans | `CALCULATE(COUNTROWS(Loan_Details), Loan_Details[Status] = "Defaulted")` |
| High Risk Loan Amount | `CALCULATE(SUM(Loan_Details[Loan_Amount]), FILTER(Customer_Details, Customer_Details[Risk Category] = "High Risk"))` |
| High Risk Loans | `CALCULATE(COUNTROWS(Loan_Details), Customer_Details[Risk Category] = "High Risk")` |
| Loan Status Count | `COUNTROWS(Loan_Details)` |

---

## 📈 Dashboard Pages & Key Insights

### 1️⃣ Customer Demographics
**KPIs:** Total Customers, Average Income, Average Age

- **1,155** total customers | **$76.62K** average income | **44.06** average age
- Education split is fairly even across tiers: Graduate (27.97%), Postgraduate (24.76%), High School (26.84%), Doctorate (20.43%) — no single education level dominates the customer base
- Gender split: Male (42.77%), Female (40.87%), Other (16.36%)
- Credit Score by Gender & Education shows customers identifying as **"Other"** gender consistently post the **highest credit scores across every education level** (e.g., 616.28 for Doctorate holders vs. 601.26 for Female Doctorate holders) — worth investigating whether this reflects a smaller, more homogenous sample rather than a true behavioral signal
- Within each gender group, credit score does **not** scale linearly with education — High School-educated customers slightly outscore Postgraduates in the Male segment, suggesting credit score here is driven more by income/repayment behavior than by education level alone

<img width="1331" height="746" alt="image" src="https://github.com/user-attachments/assets/3f9b8340-761f-4933-bcdb-7e9997fc0b2f" />


### 2️⃣ Loan Portfolio & Performance
**KPIs:** Total Loan Amount, Average Monthly Installment, Average Interest Rate

- **$253M** total loan amount | **$2.11K** average monthly installment | **8.97%** average interest rate (range: 3.01%–15.00%)
- Loan portfolio is well-diversified by design: Personal (20.58%), Mortgage (20.22%), Small Business (20.14%), Auto (19.74%), Student (19.32%) — no single loan type creates concentration risk
- All five loan types show a similar Active/Closed/Defaulted split, meaning default risk is a **portfolio-wide issue rather than isolated to one loan category**
- Individual active and defaulted loan records (both in the $97K–$99K+ range) suggest the dataset skews toward large-ticket loans, which raises the stakes of the default rate below

<img width="1252" height="740" alt="image" src="https://github.com/user-attachments/assets/72c80835-8d99-4561-89cd-e25168e0dee8" />


### 3️⃣ Financial Risk Analysis
**KPIs:** Defaulted Loans, Defaulted Loan Amount, High-Risk Loans, High-Risk Loan Amount

- **519** defaulted loans totaling **$26.19M** | **2,547** high-risk loans totaling **$127.97M**
- Defaults by employment status: Full-time (27.95%), Unemployed (25.94%), Part-time (24.3%), Self-employed (21.81%) — **full-time employment is not a strong safeguard against default**, which challenges an assumption often built into simple underwriting rules
- High-risk loan exposure follows a similar pattern: Full-time (27.19%), Unemployed (25.87%), Self-employed (23.21%), Part-time (23.74%) — risk is spread broadly across employment categories rather than concentrated in the "obvious" segments (unemployed/self-employed)
- Credit Score vs. Customers distribution shows customer volume is heavily concentrated in the **"Good"** and **"Very Good"** bands, with far fewer customers in "Excellent" — meaning most of the portfolio sits in a mid-tier risk zone rather than at either extreme
- High-risk loan amount ($127.97M) is roughly **5x** the defaulted loan amount ($26.19M) — a large pool of loans is currently flagged as risky but hasn't defaulted yet, representing the biggest lever for proactive intervention

<img width="1337" height="745" alt="image" src="https://github.com/user-attachments/assets/0d0a1166-6db5-400e-8424-7cb3d93ec98e" />


---

## 🧠 Conclusion

The Finance Dashboard provides a unified, data-driven view of the company's lending landscape. By combining a clean data model with targeted DAX measures, it surfaces where risk actually concentrates — which turns out to be less about employment status or education level than commonly assumed, and more evenly distributed across the customer base. This reframes the underwriting question from "which segment do we avoid" to "how do we catch high-risk loans before they convert to defaults," since the high-risk pool is roughly 5x larger than the current default pool.

---

## 🧠 Skills Demonstrated

`Data Modeling` · `DAX` · `Power Query (ETL)` · `Star-Schema Design` · `Credit Risk Analysis` · `Customer Segmentation` · `KPI Design` · `Dashboard/UX Design`

---

## 🛠️ Tools & Technologies

- Power BI Desktop
- DAX (Data Analysis Expressions)
- Power Query
- Excel / CSV Data Source

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

## 🚀 How to Use

1. Clone this repository
2. Open `Financial_Dashboard.pbix` in Power BI Desktop
3. Use the **Income & Credit Score / Income & Credit Score Categories / Income & Credit Score Segments** slicers on each page to explore how risk and demographics shift across income and credit bands

---

## 🔮 Future Improvements

- Build a logistic regression or scorecard model to predict default probability, then compare its output against the current "High Risk" tagging logic
- Add a cohort view tracking loans by issue-date vintage to see whether default rates are worsening or improving over time
- Break down the "Other" gender segment's high credit scores by sample size to confirm whether the pattern holds at scale

---

## 👤 Author

**Karan Kumar Sahu**
Data Analyst | SQL · Python · Power BI
