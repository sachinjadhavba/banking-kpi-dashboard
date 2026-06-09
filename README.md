# Banking KPI Dashboard Framework
### Reusable MIS & KPI Framework for Banks and Fintech Lending Portfolios

[![Excel](https://img.shields.io/badge/Excel-Advanced-217346?style=flat&logo=microsoftexcel)](https://microsoft.com/excel)
[![PowerBI](https://img.shields.io/badge/Power_BI-DAX-F2C811?style=flat&logo=powerbi)](https://powerbi.microsoft.com)
[![Domain](https://img.shields.io/badge/Domain-Banking_Analytics-1F4E79?style=flat)](https://finsight-one-4cao.vercel.app/)
[![Author](https://img.shields.io/badge/Author-Sachin_Jadhav-2E75B6?style=flat)](https://www.linkedin.com/in/sachin-jadhav-consulting)

---

## Overview

A **production-ready KPI and MIS dashboard framework** for banking and fintech portfolio management — built from 9 years of designing and presenting these dashboards to C-suite leadership at IndusInd Bank.

This repository provides:
- Complete KPI taxonomy for SME and commercial lending portfolios
- Excel template with dynamic dashboards (no macros — pure formulas + pivot)
- Power BI DAX measures library for banking metrics
- Methodology documentation for each metric

> Used as the basis for monthly C-suite portfolio review presentations across ₹500 Crore+ portfolios.

---

## Repository Structure

```
banking-kpi-dashboard/
│
├── excel/
│   ├── SME_Portfolio_KPI_Dashboard.xlsx     # Main dashboard template
│   ├── NPA_Monitoring_Dashboard.xlsx        # NPA-specific monitoring
│   └── Regional_Performance_Tracker.xlsx   # Multi-location performance
│
├── powerbi/
│   ├── Portfolio_Analytics.pbix            # Power BI report file
│   └── DAX_Measures_Library.md             # All DAX formulas documented
│
├── methodology/
│   ├── kpi_definitions.md                  # Precise definitions for each KPI
│   ├── npa_classification_guide.md         # RBI NPA classification guidelines
│   └── ewi_framework.md                    # Early warning indicator setup
│
├── templates/
│   └── Executive_Summary_Template.docx    # Board/leadership report template
│
└── README.md
```

---

## KPI Framework — What's Measured

### Portfolio Growth KPIs
| KPI | Formula | Frequency |
|-----|---------|-----------|
| Disbursement Volume | Sum of all new loans sanctioned | Monthly |
| Portfolio Outstanding | Total live book value | Monthly |
| Net Portfolio Growth | (Current - Previous) / Previous × 100 | Monthly |
| Ticket Size Distribution | Count by bucket: <50L / 50-200L / 200L+ | Monthly |

### Asset Quality KPIs
| KPI | Formula | Frequency |
|-----|---------|-----------|
| Gross NPA Ratio | Gross NPA / Gross Advances × 100 | Monthly |
| Net NPA Ratio | Net NPA / Net Advances × 100 | Monthly |
| Slippage Rate | New NPAs this period / Prev Standard Assets × 100 | Monthly |
| Recovery Rate | Recoveries / Opening NPA × 100 | Monthly |
| PCR (Provision Coverage) | Provisions / Gross NPA × 100 | Quarterly |

### Productivity KPIs
| KPI | Formula | Frequency |
|-----|---------|-----------|
| Disbursement per RM | Total Disbursement / Active RMs | Monthly |
| Portfolio per RM | Total Portfolio / Active RMs | Monthly |
| New Client Acquisition | Count of new accounts booked | Monthly |
| Fee Income per RM | Total fee income / Active RMs | Monthly |
| TAT (Sanction to Disbursal) | Avg days from sanction to first disbursal | Monthly |

### Revenue KPIs
| KPI | Formula | Frequency |
|-----|---------|-----------|
| Net Interest Margin | NII / Average Interest-Earning Assets × 100 | Monthly |
| Fee Income | Processing fees + renewal fees + other charges | Monthly |
| Yield on Advances | Interest Income / Average Advances × 100 | Monthly |
| Cost of Credit | Provisions / Average Portfolio × 100 | Monthly |

---

## Key DAX Measures (Power BI)

```dax
-- Gross NPA Ratio
NPA Ratio % = 
DIVIDE(
    CALCULATE(SUM(Portfolio[Outstanding]), Portfolio[DPD] >= 90),
    SUM(Portfolio[Outstanding]),
    0
) * 100

-- MoM Portfolio Growth
MoM Growth % = 
VAR CurrentMonth = SUM(Portfolio[Outstanding])
VAR PrevMonth = CALCULATE(SUM(Portfolio[Outstanding]), DATEADD(Date[Date], -1, MONTH))
RETURN DIVIDE(CurrentMonth - PrevMonth, PrevMonth, 0) * 100

-- Slippage Rate
Slippage Rate % =
DIVIDE(
    CALCULATE(SUM(Portfolio[Outstanding]), 
              Portfolio[DPD] >= 90,
              Portfolio[Prev_DPD] < 90),
    CALCULATE(SUM(Portfolio[Outstanding]),
              DATEADD(Date[Date], -1, MONTH),
              Portfolio[DPD] < 90),
    0
) * 100

-- Collection Efficiency
Collection Efficiency % =
DIVIDE(
    SUM(Collections[Amount_Collected]),
    SUM(Collections[Amount_Due]),
    0
) * 100
```

---

## How to Use

**Excel Dashboards:**
1. Download `SME_Portfolio_KPI_Dashboard.xlsx`
2. Paste your portfolio data into the `Data` sheet
3. All dashboards update automatically via pivot tables and formulas

**Power BI:**
1. Open `Portfolio_Analytics.pbix` in Power BI Desktop
2. Connect to your data source (Excel / SQL / CSV)
3. Refresh — all visuals and DAX measures update automatically

---

## About the Author

**Sachin Jadhav** — built and presented these dashboards to C-suite teams monthly across a ₹500 Crore regional portfolio for 9 years at IndusInd Bank.

- 🌐 [FinsightOne](https://finsight-one-4cao.vercel.app/)
- 💼 [LinkedIn](https://www.linkedin.com/in/sachin-jadhav-consultant)
- 📧 jadhav.sachin6290@gmail.com
- 📅 [Book a discovery call](https://calendly.com/jadhav-sachin6290)

---

*Every KPI definition and DAX measure here has been validated in live banking operations.*

Attribution
Domain framework: Sachin Jadhav — 19 years SME/MSME credit appraisal and portfolio management, IndusInd Bank, CSB Bank, ING Vysya Bank, Yes Bank, South Indian Bank, Axis Bank.

Code: Developed with AI assistance (Claude by Anthropic). The analytical logic, trigger thresholds, and portfolio concepts are based on real banking experience. The Python implementation was built with AI tools.

This is honest. The framework is mine. The code is assisted.
