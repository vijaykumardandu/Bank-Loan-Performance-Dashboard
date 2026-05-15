# Bank Loan Performance Dashboard

> A 4-page interactive Power BI dashboard analysing 38,600+ bank loan applications — built to replace static monthly reports with real-time portfolio monitoring, risk tracking, and stakeholder-ready insights.

---

## Problem Statement

Bank lending teams rely heavily on static spreadsheet reports that are slow to update, hard to filter, and offer no drill-down capability. This project replaces that approach with an interactive dashboard suite that lets stakeholders monitor portfolio health, spot risk trends, and investigate individual loan accounts in real time — without needing to request a new report each time.

---

## Objective

Design and develop a 4-page Power BI report enabling stakeholders to:

- Monitor portfolio KPIs with Month-to-Date (MTD) and Month-over-Month (MoM) tracking
- Classify and compare Good vs Bad loan performance across the portfolio
- Identify trends across time, geography, borrower profile, and loan purpose
- Drill down to individual loan-level records for operational or compliance investigation

---

## Dashboard Pages

### Page 1 — Executive Summary

High-level KPI cards giving a snapshot of overall portfolio health.

| KPI | Total | MTD | MoM Change |
|-----|-------|-----|------------|
| Total Loan Applications | 38.6K | 4.3K | +6.9% |
| Total Funded Amount | $435.8M | $54.0M | +13.0% |
| Total Amount Received | $473.1M | $58.1M | +15.8% |
| Average Interest Rate | 12.0% | 12.4% | +3.5% |
| Average DTI | 13.3% | 13.7% | +2.7% |

**Good vs Bad Loan Breakdown:**

| Category | Applications | Funded Amount | Received Amount |
|----------|-------------|---------------|-----------------|
| Good Loans (Fully Paid + Current) | 87.9% | $7.4M | $8.8M |
| Bad Loans (Charged Off) | 12.1% | $999.5K | $576.2K |

Loan status grid view segments portfolio into **Fully Paid**, **Charged Off**, and **Current** — each showing funded amount, received amount, average interest rate, and average DTI.

---

### Page 2 — Trends & Overview

Interactive visualisations surfacing lending trends and borrower demographics.

- **Monthly Trend (Line Chart):** Application volume grew from 2.3K (Jan) → 4.0K (Dec), revealing seasonality and H2 acceleration
- **Regional Analysis (Filled Map):** Geographic distribution across US states — highlights high-concentration lending regions
- **Loan Term Split (Donut Chart):** 73.2% on 60-month terms vs 26.8% on 36-month terms
- **Employment Length (Bar Chart):** Borrowers with 10+ years employment = largest segment (8.9K)
- **Loan Purpose (Bar Chart):** Debt consolidation dominates (18K), followed by credit card (5K) and home improvement (3K)
- **Home Ownership (Tree Map):** Rent (18K) vs Mortgage (17K) vs Own

**Filters:** State · Grade · Good vs Bad Loan · Select Measure

---

### Page 3 — Detailed Insights

Drill-down table for individual loan-level investigation.

**Columns:** Loan ID · Purpose · Home Ownership · Grade · Sub Grade · Issue Date · Funded Amount · Interest Rate · Instalment · Received Amount

**Filters:** State · Grade · Good vs Bad Loan

Supports account-level audit, compliance checks, and operational review without exporting to Excel.

---

### Page 4 — Introduction & Documentation

Project scope, KPI definitions, dashboard objectives, and implementation notes — structured for non-technical stakeholder onboarding.

---

## Tools & Technologies

| Tool | Usage |
|------|-------|
| Power BI Desktop | Dashboard development, DAX measures, interactive visuals |
| SQL / MySQL | Data extraction, joins, aggregations, KPI validation queries |
| Microsoft Excel | Data cleaning, validation, preliminary analysis |

---

## Dataset Overview

| Attribute | Detail |
|-----------|--------|
| Total Records | 38,600+ loan applications |
| Portfolio Value | $435.8M funded |
| Repayments Tracked | $473.1M received |
| Loan Statuses | Fully Paid · Charged Off · Current |
| Key Fields | Loan ID, Purpose, Grade, Sub Grade, Home Ownership, Issue Date, Funded Amount, Interest Rate, Instalment, Received Amount, DTI |

---

## Key DAX Measures

```dax
-- Month-to-Date Loan Applications
MTD Loan Applications = TOTALMTD(COUNT(loan_data[id]), 'Date'[Date])

-- Month-over-Month Change %
MoM Applications % =
VAR CurrentMonth = [MTD Loan Applications]
VAR PreviousMonth = CALCULATE([MTD Loan Applications], DATEADD('Date'[Date], -1, MONTH))
RETURN DIVIDE(CurrentMonth - PreviousMonth, PreviousMonth)

-- Good Loan Percentage
Good Loan % =
DIVIDE(
    CALCULATE(COUNT(loan_data[id]), loan_data[loan_status] IN {"Fully Paid", "Current"}),
    COUNT(loan_data[id])
)

-- Bad Loan Percentage
Bad Loan % =
DIVIDE(
    CALCULATE(COUNT(loan_data[id]), loan_data[loan_status] = "Charged Off"),
    COUNT(loan_data[id])
)
```

---

## Key Insights

- Loan applications grew **74% over the year** (Jan: 2.3K → Dec: 4.0K), indicating strong demand acceleration in H2
- **87.9% of loans are performing** (Good), with a 12.1% charge-off rate that is manageable but warrants ongoing monitoring
- **Debt consolidation** accounts for ~46% of all loan purposes, suggesting most borrowers are refinancing existing debt rather than funding new purchases
- Borrowers with **10+ years of employment** represent the single largest applicant segment (8.9K) — a positive credit risk indicator
- **60-month term loans dominate** (73.2%), meaning portfolio cash flows are longer-duration and more exposed to interest rate movements
- Charged Off loans carry a higher average DTI (13.63%) vs Fully Paid loans (12.66%) — confirming DTI as a meaningful risk differentiator that could inform future approval criteria

---

## Project Structure

```
bank-loan-dashboard/
│
├── data/
│   └── bank_loan_data.csv              # Raw loan dataset
│
├── sql/
│   └── loan_kpi_queries.sql            # SQL queries for KPI extraction and validation
│
├── dashboard/
│   └── bank_loan_data_insights.pbix    # Power BI report file
│
├── screenshots/
│   ├── summary.png
│   ├── overview.png
│   └── details.png
│
└── README.md
```

---

## How to Use

1. Clone this repository
   ```bash
   git clone https://github.com/YOUR_USERNAME/bank-loan-dashboard.git
   ```
2. Open `bank_loan_data_insights.pbix` in Power BI Desktop
3. If prompted, update the data source path to point to `data/bank_loan_data.csv`
4. Refresh the dataset — all visuals and DAX measures will populate automatically
5. Use the slicers (State, Grade, Good vs Bad Loan) to explore the data across all pages

---

## Dashboard Screenshots

### Executive Summary
<img width="2224" height="1249" alt="Screenshot 2026-05-15 104431" src="https://github.com/user-attachments/assets/7edcdeea-b123-43e0-a1ec-18f90d7a4320" />

### Trends & Overview
<img width="2221" height="1247" alt="Screenshot 2026-05-15 104342" src="https://github.com/user-attachments/assets/10732ffe-5ade-42c4-a2be-c5e282dc9851" />

### Detailed Insights
<img width="2217" height="1234" alt="Screenshot 2026-05-15 104457" src="https://github.com/user-attachments/assets/c6e5320b-7441-422d-8a08-95d38316a481" />

---

## Skills Demonstrated

- **Data modelling:** Built relationships across loan, date, and status tables; created a dedicated date table to enable time intelligence functions (MTD, MoM)
- **DAX:** Wrote measures for MTD totals, MoM percentage change, and Good/Bad loan classification using `TOTALMTD`, `DATEADD`, `CALCULATE`, and `DIVIDE`
- **Dashboard design:** Structured 3 audience-specific views — executive summary for leadership, trends overview for analysts, and a drill-down details table for operations teams
- **Data cleaning:** Validated and reconciled raw loan records in Excel before loading into Power BI; handled null values, inconsistent date formats, and duplicate entries
- **Stakeholder thinking:** Designed each page with a specific user in mind — KPI cards for quick scanning, slicers for self-service filtering, and commentary-ready visuals for reporting

---

## Author

**Dandu Vijay Kumar**
- LinkedIn: [linkedin.com/in/vijaykumar841](https://linkedin.com/in/vijaykumar841)
- Email: danduvijaykumar841@gmail.com

---

*This project was built for portfolio and learning purposes.*
