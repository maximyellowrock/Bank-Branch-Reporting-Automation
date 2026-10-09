<div align="center">

# 🏦 BranchFlow
### Bank Branch Reporting Automation | Excel + Power Query

**Financial Reporting · Power Query ETL · YTD & YoY Analysis · Automated Reconciliation**

![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)
![Power Query](https://img.shields.io/badge/Power_Query-0078D4?style=for-the-badge)
![Financial Reporting](https://img.shields.io/badge/Financial_Reporting-334155?style=for-the-badge)

[![Watch the BranchFlow demo](https://img.youtube.com/vi/C1tumI_WpaQ/hqdefault.jpg)]([https://youtu.be/C1tumI_WpaQ](https://youtu.be/3h3Hl6exknc?si=UYtLRAI49QWzfeAg))

### ▶️ [Watch the complete project demonstration]([https://youtu.be/C1tumI_WpaQ](https://youtu.be/3h3Hl6exknc?si=UYtLRAI49QWzfeAg))

</div>

---

## 📌 Project Overview

**BranchFlow** is a portfolio project demonstrating an automated monthly financial reporting workflow for a fictional retail bank. Built with **Microsoft Excel, Power Query (M) and dynamic Excel formulas**, it transforms separate monthly source sheets into consistent branch-level analysis, management dashboards and data-quality checks.

The demo covers **24 months (January 2024–December 2025)**. All bank names, branch names and financial figures are **fictional**.

> **Repository scope:** The fictional demo dataset is shared for illustration. The completed automation workbook and its full Power Query implementation are not distributed; the end-to-end workflow is shown in the video above.

## 🎯 The Business Problem

Monthly branch reporting often involves repetitive manual tasks:

- Consolidating separate monthly Excel worksheets.
- Correcting inconsistent branch names across reporting periods.
- Calculating year-to-date income while treating month-end balances correctly.
- Preparing prior-year and month-on-month comparisons.
- Checking manually entered totals and investigating differences.
- Keeping management reports and chart data up to date.

**Goal:** Replace fragile copy-and-paste reporting with a repeatable workflow that is easier to refresh, review and validate.

## 📊 Demo Scope & Results

| Measure | Demonstration |
|---|---:|
| Reporting history | 24 months |
| Reporting years | 2024 and 2025 |
| Branches in the demo | 18 |
| Loan product categories | 4 |
| Financial metrics per product | 3 |
| Normalised records in `Fact_Assets` | **5,184** |
| Automated reconciliation checks | **288** |
| Intentionally introduced discrepancies detected | **10** |

The 10 discrepancies were deliberately inserted into the fictional source data to test the validation logic. Suggested reasons for a discrepancy are investigative leads, **not confirmed root causes**.

## ⚙️ How BranchFlow Works

```text
Monthly Excel source sheets (Jan 2024 ... Dec 2025)
                        |
                        v
               Power Query (M)
          Consolidate · Unpivot · Clean
                        |
             +----------+----------+
             |                     |
             v                     v
       Fact_Assets           Check_TypedTotals
             |                     |
        Branch_Map             Validation
             |
             v
      Dynamic YTD / YoY
             |
       +-----+------+
       |            |
       v            v
     Summary     Chart_Feed
```

### Core Capabilities

**1. Automated data preparation**  
Power Query consolidates monthly worksheets, reshapes loan-product fields into a long-format fact table and standardises branch names using a mapping table. Unmapped branch names are flagged instead of silently discarded.

**2. Financial reporting logic**  
Gross loan balances (**MEBS**) use the selected month's closing balance. **Net Interest Income (NII)** and **Net Fee Income (NFI)** accumulate from January to the selected reporting month. The model also supports available year-over-year and month-on-month comparisons.

**3. Dynamic management dashboard**  
Changing the **reporting year and month** updates KPI cards, product summaries, branch rankings, trend charts and data-quality indicators.

**4. Automated reconciliation**  
Source `TOTAL BRANCHES` figures are checked against calculated branch totals. Differences receive an **OK / CHECK** status and explanatory notes to support investigation.

**5. Presentation-ready chart feeds**  
A fixed-layout `Chart_Feed` worksheet provides stable source ranges for Excel charts and potential links to PowerPoint / think-cell presentations.

**6. Reusable source configuration**  
A `Settings` worksheet supplies the data file path to Power Query, allowing the source workbook to be relocated without manually editing the M code.

## 🗂️ Workbook Components

| Worksheet | Purpose |
|---|---|
| `Summary` | Executive KPIs, reporting-period selectors, financial comparisons, branch rankings, charts and alerts. |
| `Fact_Assets` | Normalised monthly financial records loaded through Power Query. |
| `Branch_Map` | Raw-to-standard branch name and city mapping. |
| `YTD` | Branch-level month-end balances, cumulative income and prior-period comparisons. |
| `Validation` | Reconciliation of typed totals against independently calculated totals. |
| `Chart_Feed` | Fixed-layout financial data tables for charting and presentations. |
| `Settings` | Configurable source workbook path. |

## 📈 Example Reporting Output

*Illustrative results for December 2025 from the fictional dataset:*

| KPI | Value |
|---|---:|
| Gross Loans (MEBS) | 6,501,144.89 |
| Net Interest Income — YTD | 342,307.44 |
| Net Fee Income — YTD | 112,410.13 |
| NII + NFI — YTD | 454,717.57 |

## 🧰 Tools & Techniques

`Microsoft Excel` · `Power Query (M)` · `Data Transformation` · `Unpivot` · `Merge / Mapping` · `Dynamic Arrays` · `SUMIFS` · `YTD / YoY / MoM Analysis` · `Financial Reconciliation` · `Exception Reporting` · `Excel Charts`

## 📁 Repository Contents

- **`README.md`** — project description, architecture and results.
- **`Bank_Demo_Data.xlsx`** — fictional monthly source data, if published under this filename.
- **[Video demonstration](https://youtu.be/C1tumI_WpaQ)** — walkthrough of the complete automation workbook and reporting process.

The completed automation workbook is **not** provided for download. This repository is a **portfolio demonstration**, not a ready-to-run distribution of the full solution.

## ⚠️ Notes & Limitations

- All data is synthetic; the project does not use real bank or client records.
- The earliest reporting year has no prior-year data, so comparisons requiring 2023 are shown as unavailable.
- A newly added branch may need review in the mapping table before branch-level reporting is finalised.
- Results and process improvements are demonstrated in a simulation; no live-client time savings are claimed.

---

<div align="center">

**Created by [Maxim Irinov](https://github.com/maximyellowrock)**  
*Financial Analytics · Business Intelligence · Reporting Automation*

▶️ **[BranchFlow Video Demo](https://youtu.be/C1tumI_WpaQ)**

</div>
