# BranchFlow - Bank Branch Reporting Automation (Excel + Power Query)

A monthly branch reporting workflow for a retail bank, rebuilt in Excel.
Manual cell linking is replaced by Power Query. The demo holds 24 months of data (Jan 2024 - Dec 2025). You pick a year and a month, and the whole report follows, with year-over-year comparison. Typed totals are checked automatically.

> All data in this repository is fictional (Northwind Bank, invented branches, cities and numbers).

## The problem

Every month, the finance team:

- copied branch data from monthly sheets and linked cells by hand to build a YTD file,
- fixed inconsistent branch names manually,
- typed product totals by hand (errors were hard to find),
- updated charts in PowerPoint, and the chart links often broke.

## Before vs after

| | Before | After |
|---|---|---|
| Combine monthly data | Manual copy and cell links | Power Query, one click (Refresh All) |
| Branch names | Fixed by hand every month | Mapping table, fixed once |
| YTD figures | Rebuilt every month | Two input cells (reporting year + month) |
| Last-year comparison | Separate file, copied by hand | Automatic YoY and MoM for every product and branch |
| Typed totals | Errors found late, or never | Every total checked, with a comment explaining the gap |
| Charts | Links break when rows change | Fixed-layout Chart_Feed sheet, links stay stable |
| Time per month | About 2-3 days | About 2 hours (refresh + review) |

*Time estimates are for a typical monthly cycle, not measured on a real client.*

## What is inside `Bank_Automation.xlsx`

| Sheet | What it does |
|---|---|
| **Summary** | One-page report: KPI cards with MoM and YoY change, product summary vs last year, top 5 branches, a watch line for loss-making branches, the data checks to review for the selected year, a monthly trend chart (this year vs last year) and a top-branches chart. Year (C4) and month (C5) are set here. |
| **Validation** | Compares hand-typed TOTAL rows with calculated branch totals. Each mismatch gets a status (OK / CHECK) and a plain-English comment. If the gap equals one branch exactly, the comment names it, for example *"Typed total is higher by 459,733 - equals Ardenvale Westgate: branch counted twice?"*. Otherwise it flags a likely typing error. |
| **Chart_Feed** | Fixed-layout output tables for charts (Excel charts or think-cell): product summary, 12-month trend (this year vs last year) and KPI comparison. The layout never changes, so chart links do not break. |
| **Fact_Assets** | Power Query output: every month sheet (named like "Jan 2025") unpivoted into one long table (Month, Branch, City, Product, Metric, Value, MonthNum, Year, Period). Other sheets in the data file are ignored. New month sheets are picked up automatically. |
| **Branch_Map** | Mapping table from raw, inconsistent branch names to one clean name and a city. A branch missing here is not lost: it comes through as "<raw name> (UNMAPPED)", and Summary and Validation show a warning. |
| **YTD** | Branch-level report for the selected year. The branch list comes from the data itself (dynamic array), so new or unmapped branches appear automatically. Balances (MEBS) use the selected month only. Income (NII, NFI) is summed from January, and compared with the same period last year. |

| **Settings** | `Source_Path` cell used by Power Query. By default it points to `Bank_Demo_Data.xlsx` in the same folder as this workbook, so no query editing is needed. |

Metrics: **MEBS** = month-end balance (gross loans), **NII** = net interest income, **NFI** = net fee income.

## How to run

1. Download `Bank_Automation.xlsx` and `Bank_Demo_Data.xlsx` into the same folder.
2. Open `Bank_Automation.xlsx` (Microsoft 365 / Excel 2021 or later).
3. Nothing else to set: the **Settings** sheet finds the data file in the same folder. (Other folder or file name? Change it on the Settings sheet.)
4. **Data > Refresh All**. The demo file is set to ignore privacy levels, so it refreshes without prompts. For client data, set both sources to the right privacy level instead (for example Organizational): **Data > Get Data > Data Source Settings > Edit Permissions**.
5. On the **Summary** sheet, set the year in C4 (2024 or 2025) and the month in C5 (1 = Jan ... 12 = Dec). Every sheet and chart follows.

## Known limits

- Year-over-year needs the prior year in the data. For 2024 (the first year in the demo) the report shows "n/a" / "No prior-year data" instead of a comparison.
- A branch missing from Branch_Map is not lost: it shows in the YTD table and rankings as "<raw name> (UNMAPPED)", and a warning appears. Add it to Branch_Map to give it a clean name and city.
- `Source_Path` must be a local or network folder path. OneDrive/SharePoint web addresses (https) do not work with this setup.

## Monthly process after automation

1. Add the new month sheet to the data file, named like "Jan 2026" (same layout).
2. **Data > Refresh All**.
3. Set the reporting year and month on Summary.
4. Review the data checks and fix the source if needed.
5. Charts update automatically. think-cell users link their charts to Chart_Feed once.

## Power Query code

The M code of all three queries is in `Section1.m` (Fact_Assets, tblBranchMap, Check_TypedTotals).

## Tools and techniques

Excel (Microsoft 365) · Power Query (M) · Unpivot · Merge with mapping table · SUMIFS with dynamic arrays · structured table references · AGGREGATE for exception lists · LOOKUP(2,1/...) multi-criteria lookup · conditional formatting · data validation · reconciliation logic · native Excel charts · think-cell-ready output design
