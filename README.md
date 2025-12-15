# 🌴 Palm Oil Profitability Feasibility Study  
## Realistic Investment Modeling & Interactive Dashboard Simulation (Nigeria)

**Prepared by:**  
**Data Analyst:** Ibemgbo Success  

---

## 🛠️ Tools Used
- 🐍 **Python (Jupyter Notebook)**
- 📗 **Microsoft Excel**
- 📊 **Microsoft Power BI**
- 📄 **Google Docs**

**Date:** November 2025  

---

## 📑 Table of Contents
- [Executive Summary](#1-executive-summary)
- [Data Collection and Preparation](#2-data-collection-and-preparation)
  - [2.1 Data Sources](#21-data-sources)
  - [2.2 Data Preparation Process](#22-data-preparation-process)
- [Modeling and Scenario Simulation](#3-modeling-and-scenario-simulation)
  - [3.1 Python Modeling Overview](#31-python-modeling-overview)
- [Power BI Interactive Simulator Design](#4-power-bi-interactive-simulator-design)
  - [4.1 Data Import](#41-data-import)
  - [4.2 What-If Parameters](#42-what-if-parameters)
- [Dashboard Layout and Visualization](#5-dashboard-layout-and-visualization)
- [Results and Key Findings](#6-results-and-key-findings)
- [Business Recommendation](#7-business-recommendation)
- [Assumptions and Limitations](#assumptions-and-limitations)
- [Data Needs for Live Investor-Grade Analysis](#data-needs-for-live-investor-grade-analysis)
- [Conclusion](#8-conclusion)
- [References](#references)

---

## 1. Executive Summary

This report presents a **data-driven investment feasibility analysis** of Nigeria’s palm oil sector using a combination of **real-world data** and **proxy-based financial simulation**.

The analysis estimates the **scale, cost, yield, and financial viability parameters** required for a palm oil plantation to achieve an **annual profit target of ₦1 billion**.

---

### Scope of Analysis

Data from **six major palm-oil-producing states** were analyzed:

- Edo  
- Delta  
- Rivers  
- Akwa Ibom  
- Cross River  
- Ondo  

The model integrates:

- Real market data from **FAO** and **Jiji.ng**
- Proxy agricultural cost benchmarks
- Python-based financial modeling
- Interactive **Power BI What-If simulations**

---

### Key Finding

> **Edo State** emerges as the most profitable investment destination, generating an estimated  
> **₦16.04 million per hectare (base scenario)**, driven by:
- High yield efficiency (**≈ 16.22 t/ha**)
- Favorable rainfall (**≈ 2,490 mm/year**)

---

## 2. Data Collection and Preparation

### 2.1 Data Sources

To ensure realistic modeling inputs, three primary datasets were curated.

| Dataset | Description | Source |
|------|------------|-------|
| `state_factors.csv` | Yield, cost, rainfall, land metrics by state | FAO (2024), Okomu Oil PLC Annual Report, Presco PLC Investor Factsheet |
| `market_prices.csv` | Palm oil price per tonne (scenario-based) | Jiji.ng Wholesale Listings, FAOSTAT |
| `scenario_results.csv`<br>`npv_irr_by_state_mature.csv` | Profitability, NPV, IRR outputs | Author’s Analysis (2025) |

---

### Pricing Assumptions

- **Conservative:** ₦900,000 / tonne  
- **Base:** ₦1,050,000 / tonne  
- **Optimistic:** ₦1,200,000 / tonne  

> **Note:**  
> Approximately **40%** of the data was sourced directly from verified public datasets, while  
> **60%** was derived using **proxy estimation and cost scaling** based on industrial benchmarks.

---

### 2.2 Data Preparation Process

All datasets were cleaned, merged, and transformed using **Python (pandas, numpy)** in **Jupyter Notebook**.

#### Data Preparation Steps
- Missing rainfall and yield values interpolated using FAO regional averages  
- Land acquisition and plantation establishment costs amortized over **25 years**  
- Mature yield assumptions applied:
  - Plantation maturity begins from **Year 4**
  - Average yield ≈ **3–4 t/ha annually**

#### Scenario Multipliers
Conservative: Yield × 0.90 | Cost × 1.05
Base:         Yield × 1.00 | Cost × 1.00
Optimistic:  Yield × 1.15 | Cost × 0.95

The final output dataset was exported to **Power BI**, where the following were created for convenient UI/UX simulation:

- Core modeling parameters  
- Measures  
- Tables  
- A simple green-light dashboard  

---

## 3. Modeling and Scenario Simulation

### 3.1 Python Modeling Overview

Two major modeling blocks were implemented:

---

### 1️⃣ Profitability Simulation Model

This model computes, **per state**:

- Revenue per hectare  
- Cost per hectare  
- Profit per hectare  
- ROI  
- Payback period  

The target profit was fixed at **₦1,000,000,000**, and the required plantation size was calculated as:

``math
\text{Hectares Needed} =
\frac{₦1,000,000,000}{\text{Profit per hectare}}
### 2️⃣ Financial Viability Model (NPV & IRR)

- 20-year cashflow model  
- Yield ramp-up from **0% → 100% by Year 5**  
- Discount rate: **12%**

#### Investment Viability Rule
- Positive **Net Present Value (NPV)**  
- **IRR > 12%**

States meeting both conditions were classified as **investment-viable**.

---

## 4. Power BI Interactive Simulator Design

<img width="494" height="225" alt="Screenshot 2025-11-12 173325" src="https://github.com/user-attachments/assets/f9dd48df-3623-4a2d-8dec-a371196bba66" />


### 4.1 Data Import

**Merged Dataset:**  
`powerbi_investor_dataset.xlsx`

**Tables Used:**
- `State_Factors`
- `ScenarioResults`
- `NPV_IRR_by_State_Mature`

All tables were linked using:
- **State**
- **Scenario**

---

### 4.2 What-If Parameters

| Parameter | Range | Purpose |
|---------|------|--------|
| Planned_Hectares | 0 – 1000 | Simulate plantation scale |
| YieldPctAdj | –50% to +50% | Climate & technology sensitivity |
| CostPctAdj | 0 – 1000% | Cost stress-testing |

---

### Core DAX Measures

``DAX
Adj_Yield_ha =
SELECTEDVALUE(State_Factors[Yield_t_ha]) *
(1 + SELECTEDVALUE(YieldPctAdj[YieldPctAdj Value]) / 100)

Adj_Cost_ha =
SELECTEDVALUE(State_Factors[Cost_per_ha]) *
(1 + SELECTEDVALUE(CostPctAdj[CostPctAdj Value]) / 100)

Total_Revenue =
[Adj_Yield_ha] *
SELECTEDVALUE(Market_Prices[Price_per_t]) *
[Planned_Hectares]

Total_Costs =
[Adj_Cost_ha] * [Planned_Hectares]

Adj_Profit_per_ha =
[Total_Revenue] - [Total_Costs]

## 5. Dashboard Layout and Visualization

<img width="1493" height="839" alt="Screenshot 2025-11-13 220651" src="https://github.com/user-attachments/assets/d46b4b3f-4241-47f5-bc73-4e0a2b0cc4f5" />


---

### Dashboard Structure (Single Page)

| Section | Visualization | Description |
|------|--------------|-------------|
| Header KPIs | Cards | Revenue, Adjusted Profit/ha, ROI, Yield/ha, Cost, Break-even Ha |
| Profit Target | Gauge | Total profit vs ₦1bn target |
| Profit per State | Horizontal Bar | Edo leads with ₦16.04m/ha |
| Revenue vs Cost | Clustered Columns | State-level cost structure |
| Yield vs Rainfall | Bubble Scatter | Yield efficiency by rainfall |
| Scenario Filters | Slicers | Scenario & State selector |
| Parameter Panel | Sliders | Interactive What-If controls |

All visuals update dynamically with slider adjustments.

---

## 6. Results and Key Findings

### 1️⃣ Edo State

- Mature yield: **≈ 8 t/ha**
- Avg rainfall: **≈ 2,490 mm**
- Profit per ha: **₦16.04 million**
- IRR: **≈ 19%**

**Most profitable and sustainable investment location**

---

### 2️⃣ Akwa Ibom & Delta

- Profit per ha: **₦4–5 million**
- High rainfall (**1,871–2,487 mm**)

**Second-tier opportunities for mid-scale plantations**

---

### 3️⃣ Cross River & Ondo

- Lower yields and rainfall  
- Positive but thin ROI margins  

---

### 4️⃣ Scenario Sensitivity

- **Optimistic:** Profit increases ≈ 25%  
- **Conservative:** ROI drops below 10%  
- **Base:** ₦1bn profit achievable at **≈ 62–65 ha**

---

## 7. Business Recommendation

### Top 3 Investment States

| Rank | State | Profit/ha (₦m) | Rainfall (mm) | Remark |
|----|------|---------------|--------------|--------|
| 1 | Edo | 16.04 | 2490 | Best ROI |
| 2 | Akwa Ibom | 4.15 | 2487 | Stable |
| 3 | Delta | 4.00 | 1871 | Growing demand |

---

### Minimum Viable Plantation Size

- **60–70 hectares** required to generate **₦1bn annual profit** (Base case)

---

### Investment Budget Estimate

| Cost Component | Per ha (₦m) | 62 ha (₦bn) |
|--------------|------------|-------------|
| Land + Establishment | 10.36 | 0.64 |
| Annual O&M + Processing | 0.30 | 0.02 |
| Working Capital & Buffer | — | 0.10 |
| **Total Initial Investment** | — | **₦0.76 bn** |

---

## Assumptions and Limitations

- Price volatility and market risk  
- Climate and rainfall variability  
- Proxy-estimated data (**~60%**)  
- Land cost variations across states  

---

## Data Needs for Live Investor-Grade Analysis

- Verified yield & cost records (**Okomu, Presco, NIFOR**)  
- Local processing & logistics benchmarks  
- Continuous wholesale & export price tracking  

---

## 8. Conclusion

This project demonstrates how **data science and business intelligence** can guide agricultural investment decisions.

### Key Takeaways

- Edo State delivers the strongest ROI  
- ₦1bn annual profit achievable at **~62 ha**  
- Expansion into Akwa Ibom & Delta reduces risk  

This framework can be extended into a **live investment monitoring system** with real-time data feeds and environmental sensors.

---

## References

- **FAO (2024).** FAOSTAT Agricultural Data  
  https://www.fao.org/faostat  

- **Presco PLC (2023).** Annual Report & Financial Statements  

- **Jiji.ng (2024).** Palm Oil Wholesale Market Prices — Nigeria  
  https://www.jiji.ng  

- **Okomu Oil Palm Company PLC (2023).** Investor Relations Report  

