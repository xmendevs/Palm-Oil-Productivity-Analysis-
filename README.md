# Palm Oil Profitability Feasibility Study  
## Realistic Investment Modeling & Interactive Dashboard Simulation (Nigeria)

**Prepared by:**  
**Data Analyst:** Ibemgbo Success  

**Tools Used:**  
- Python (Jupyter Notebook)  
- Microsoft Excel  
- Microsoft Power BI  
- Google Docs  

**Date:** November 2025  

---

## Table of Contents
- [Executive Summary](#executive-summary)
- [Data Collection and Preparation](#data-collection-and-preparation)
  - [2.1 Data Sources](#21-data-sources)
  - [2.2 Data Preparation Process](#22-data-preparation-process)
- [Modeling and Scenario Simulation](#modeling-and-scenario-simulation)
  - [3.1 Python Modeling Overview](#31-python-modeling-overview)
- [Power BI Interactive Simulator Design](#power-bi-interactive-simulator-design)
  - [4.1 Data Import](#41-data-import)
  - [4.2 What-If Parameters](#42-what-if-parameters)
- [Dashboard Layout and Visualization](#dashboard-layout-and-visualization)
- [Results and Key Findings](#results-and-key-findings)
- [Business Recommendation](#business-recommendation)
- [Assumptions and Limitations](#assumptions-and-limitations)
- [Conclusion](#conclusion)
- [References](#references)

---

## Executive Summary

This report presents a **data-driven investment feasibility analysis** of Nigeria’s palm oil sector using a combination of **real-world data** and **proxy-based financial simulation**.

The analysis estimates the **scale, cost, and yield requirements** needed for a palm oil plantation to achieve an **annual profit target of ₦1 billion**.

### Key Highlights
- Six major palm-oil-producing states were analyzed:
  - Edo  
  - Delta  
  - Rivers  
  - Akwa Ibom  
  - Cross River  
  - Ondo  

- The model integrates:
  - Real market data (FAO, Jiji.ng)
  - Proxy agricultural cost benchmarks
  - Dynamic **What-If simulations** in Power BI

### Core Finding
> **Edo State** emerges as the most profitable investment location, generating an estimated **₦16.04 million per hectare** under base conditions, driven by:
- High yield efficiency (**16.22 t/ha**)  
- Favorable rainfall (~**2490 mm/year**)  

---

## Data Collection and Preparation

### 2.1 Data Sources

To ensure realism and validation, three primary datasets were curated:

| Dataset | Description | Source |
|------|------------|-------|
| `state_factors.csv` | Yield, cost, rainfall, land metrics per state | FAO (2024), Okomu Oil PLC, Presco PLC |
| `market_prices.csv` | Palm oil prices per tonne (scenario-based) | Jiji.ng, FAOSTAT |
| `scenario_results.csv` / `npv_irr_by_state_mature.csv` | Profitability & financial metrics | Author’s Analysis (2025) |

**Price Scenarios:**
- Conservative: ₦900,000 / tonne  
- Base: ₦1,050,000 / tonne  
- Optimistic: ₦1,200,000 / tonne  

> **Note:** ~40% of the data was sourced directly from verified public datasets, while ~60% was derived using proxy estimation and industrial benchmarks.

---

### 2.2 Data Preparation Process

Data cleaning and preparation were performed using **Python (pandas, numpy)** in Jupyter Notebook.

#### Steps:
1. Missing rainfall and yield values interpolated using FAO averages  
2. Land acquisition and establishment costs amortized over **25 years**  
3. Mature yield assumptions applied:
   - Plantation matures from **Year 4**
   - Average yield ≈ **3–4 t/ha**
4. Scenario multipliers applied:

```text
Conservative: Yield × 0.90 | Cost × 1.05
Base:         Yield × 1.00 | Cost × 1.00
Optimistic:  Yield × 1.15 | Cost × 0.95
