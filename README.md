# United-States-Healthcare-Dynamics-Analysis
Comprehensive Power BI analytics solution for an 11-hospital US healthcare network (2019–20). Features 5 interactive dashboards, 30 custom DAX measures, and a star schema data model covering financial performance, patient demographics, provider workforce, and COVID-19 operational impact.

### Youtube Video Link: 

## Dashboards

| Dashboard | Focus |
|---|---|
| Executive Summary | Network-wide revenue, expenses, payment KPIs, and monthly trends |
| Hospital Insights | Hospital-level IPTP/ARGE ratios, bad debts, and CPT grouping breakdown |
| Patient Analysis | Demographics, geographic distribution, blood groups, lifestyle risk profile |
| Payer-Provider Analysis | Workforce composition, specialty performance, regional provider distribution |
| Monthly Expenses Trends | Gross vs adjusted expense trajectory with scenario modelling |

## Data Model

<img width="1920" height="1080" alt="schema" src="https://github.com/user-attachments/assets/2f5252e1-e0a7-482b-8cb3-049b462e8405" />

## Key Measures used
```dax
-- Revenue
TotalPayment = SUM(FactTable[Insurance_Payment]) + SUM(FactTable[Patient_Payment])
YTDPayment   = CALCULATE([TotalPayment], DATESYTD(DimDate[Date]))
QTDPayment   = CALCULATE([TotalPayment], DATESQTD(DimDate[Date]))

-- Efficiency Ratios
IPTP Ratio   = SUM(FactTable[Insurance_Payment]) / [TotalPayment]
ARGE Ratio   = SUM(FactTable[AR]) / SUM(FactTable[Gross Expenses])

-- Time Intelligence
Previous MonthPay  = CALCULATE([TotalPayment], DATEADD(DimDate[Date], -1, MONTH))
TotalPayMA         = DIVIDE(CALCULATE([TotalPayment], DATESINPERIOD(DimDate[Date], MAX(DimDate[Date]), -10, DAY)), 10)
10DayRollingPay    = CALCULATE([TotalPatientPay], DATESINPERIOD(DimDate[Date], MAX(DimDate[Date]), -10, DAY))

-- Demographics
DistinctPatient    = DISTINCTCOUNT(FactTable[dimPatientFK])
IPTP Ratio         = SUM(FactTable[Insurance_Payment]) / [TotalPayment]
```

## Key Findings

-  **$4M network deficit** — Total expenses ($13M) exceeded total revenue ($9M) across the fiscal year
-  **89% procedure volume collapse** — COVID-19 drove patient count from 4,800 (Jan) to 200 (Dec)
-  **Genesis Hospital anomaly** — Best IPTP ratio (90%) but worst ARGE ratio (19%) in the network
-  **78,883 inactive enrollees** — Only 6% of 84,000 enrolled patients are actively generating care
-  **Northeast coverage gap** — 30% fewer providers than the South despite higher population density
-  **October expense spike** — Unexplained 5.6x gross expense surge ($0.37M → $2.06M) requires investigation


## Tools & Technologies
Power BI (PL-300 Certified)


## Dashboard Previews

| Executive Summary | Hospital Insights |
|---|---|
| ![Executive Summary](https://github.com/user-attachments/assets/83c68c5c-20e2-4d56-80f5-5376b5b6ea37) | ![Hospital Insights](https://github.com/user-attachments/assets/efc1de51-8513-4c68-a105-f7d23de77584) |

| Patient Analysis | Payer-Provider |
|---|---|
| ![Patient Analysis](https://github.com/user-attachments/assets/43379872-015e-4667-8446-3200544fed03) | ![Payer Provider Analysis](https://github.com/user-attachments/assets/c12cf51d-b2c6-4ca9-aaed-642d68dc3668) |


### License
This project is for portfolio and educational purposes. Data has been anonymized.
