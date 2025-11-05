# 💼 Finance Dashboard — Power BI Project

## 📊 Overview  
This project focuses on analyzing **customer–loan relationship data** to extract key financial insights and support data-driven decision-making. The analysis helps identify customer segments, loan performance patterns, and areas of financial risk.

The dashboard provides a comprehensive view of:  
- Customer demographics and income distribution  
- Loan portfolio performance  
- Default and high-risk loan trends  
- Loan type distribution and borrower profiles  

---

## 🎯 Business Problem & Objective  
The company aims to:  
- Identify **potential default risks** and **high-risk customers**  
- Evaluate **loan recovery opportunities**  
- Determine **optimal customer segments** for future lending  
- Understand **customer behavior patterns** based on demographics and credit profiles  

The insights will help improve **credit risk management**, **loan approval strategies**, and **profitability**.

---

## 🧾 Dataset Description  

### 1. **Customer Details**  
| Column | Description |
|---------|-------------|
| Customer ID | Unique identifier for each customer |
| Name | Customer name |
| Age | Customer age |
| Gender | Male / Female / Other |
| Income | Annual income of the customer |
| Employment Status | Full-time / Part-time / Self-employed / Unemployed |
| Educational Level | High School / Graduate / Postgraduate / Doctorate |
| Credit Score | Customer’s credit rating |

### 2. **Loan Details**  
| Column | Description |
|---------|-------------|
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
A **Date table** was created to support time-based analysis and relationships.  
Data relationships were established as follows:

- **Loan Details → Customer Details:** Many-to-One (`Customer_ID`)  
- **Loan Details → Date Table:** Many-to-One (`Issue Date`)  

This model enables seamless data slicing by time, customer, and loan attributes.

---

## 🧮 KPI Development (DAX Measures)

| KPI | DAX Formula |
|-----|--------------|
| **Average Age** | `AVERAGE(Customer_Details[Age])` |
| **Average Income** | `AVERAGE(Customer_Details[Income])` |
| **Average Interest Rate** | `AVERAGE(Loan_Details[Interest_Rate])` |
| **Average Monthly Installment** | `AVERAGE(Loan_Details[Monthly_Installment])` |
| **Total Customers** | `COUNTA(Customer_Details[Customer_ID])` |
| **Total Loan Amount** | `SUM(Loan_Details[Loan_Amount])` |
| **Defaulted Loan Amount** | `CALCULATE(SUM(Loan_Details[Loan_Amount]), FILTER(Loan_Details, Loan_Details[Status] = "Defaulted"))` |
| **Defaulted Loans** | `CALCULATE(COUNTROWS(Loan_Details), Loan_Details[Status] = "Defaulted")` |
| **High Risk Loan Amount** | `CALCULATE(SUM(Loan_Details[Loan_Amount]), FILTER(Customer_Details, Customer_Details[Risk Category] = "High Risk"))` |
| **High Risk Loans** | `CALCULATE(COUNTROWS(Loan_Details), Customer_Details[Risk Category] = "High Risk")` |
| **Loan Status Count** | `COUNTROWS(Loan_Details)` |

---

## 📈 Key Insights

### 🧍 Customer Demographics  
- **Total Customers:** 1,155  
- **Average Age:** 44 years  
- **Average Income:** $76.62K  
- Majority of borrowers are **graduates**, followed by **high school** and **postgraduates**.  
- **Female customers** outnumber male and other gender groups.  

### 💰 Loan Portfolio Overview  
- **Total Loan Amount:** ₹253M  
- **Average Monthly Installment:** ₹2.11K  
- **Average Interest Rate:** 8.97% (Min: 3%, Max: 15%)  
- **Most common loan types:** Student → Auto → Mortgage → Personal → Small Business  

### ⚠️ Risk & Default Analysis  
- **Total Defaulted Loans:** 519  
- **Total Defaulted Amount:** $26.19M  
- **Total High-Risk Loans:** 2,547  
- **Total High-Risk Loan Amount:** $127.97M  
- **Defaulted Loans:** Highest among *Self-Employed* customers, followed by *Full-time*, *Part-time*, and *Unemployed*.  
- **High-Risk Loans:** Also dominated by *Self-Employed* customers.  

---

## 🧹 Data Cleaning & Preparation  
- Removed duplicate and null records  
- Standardized column names and formats  
- Converted data types for numerical and date fields  
- Categorized customers by **risk category**, **education level**, and **employment status**  

---

## 📊 Dashboard Features  
- **KPI Cards** showing financial summaries  
- **Pie & Bar Charts** for customer segmentation (gender, education, employment)  
- **Loan Type Distribution** visualization  
- **Risk & Default Analysis** panels  
- **Interactive Filters:** Date, Loan Type, Risk Category
  <img width="1281" height="729" alt="image" src="https://github.com/user-attachments/assets/a6a9564c-df56-40ef-822c-c434bc1333eb" />
  <img width="1224" height="725" alt="image" src="https://github.com/user-attachments/assets/1197a99f-4b93-46e7-8e1f-eca385b10d97" />
  <img width="1270" height="733" alt="image" src="https://github.com/user-attachments/assets/64d3e31f-450a-4473-b5ec-cf9b2a4a9b9f" />



---

## 🧠 Conclusion  
The Finance Dashboard provides a unified and data-driven view of the company’s lending landscape.  
By leveraging **Power BI** and **DAX**, the dashboard delivers actionable insights into:  
- Loan performance and repayment patterns  
- Customer risk segmentation  
- Strategic areas for improving loan allocation and recovery  

This helps stakeholders make informed decisions on **credit risk management**, **customer targeting**, and **loan disbursement strategy**.

---

## 🛠️ Tools & Technologies  
- **Power BI Desktop**  
- **DAX (Data Analysis Expressions)**  
- **Power Query**  
- **Excel / CSV Data Source**  

