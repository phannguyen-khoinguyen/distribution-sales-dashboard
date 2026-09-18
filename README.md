# Distribution Sales Analysis Report 2022–2024 | Excel

## 1. Objective

Build a complete data processing pipeline in Excel — from raw transaction data to an interactive Dashboard — to track and analyze the sales performance of 4 distributors (**FPT, Viettel, VNPT, Company A**) across 10 products (**Product 01 – Product 10**), in 3 regions (**North / Central / South**), over the period **01/01/2022 – 31/12/2024** (~4,983 transactions).

## 2. Data Structure & Processing Flow

The workbook consists of 14 sheets, organized into 4 groups following the data processing flow:

```
Raw Data  →  Calculations  →  Aggregation (Pivot)  →  Visualization (Dashboard)
```

| # | Sheet | Role |
|---|-------|------|
| 1 | `Input Price` | Input price table (million VND) for each product SP 01–SP 10 |
| 2 | `Coefficient` | Sales cost coefficient & profit coefficient by distributor, split into 2 product groups (SP01–05, SP06–10) |
| 3 | `Price` | Quick-reference summary table (combines the two tables above) |
| 4 | `Data` | **Raw transaction data**: Date, Region, Distributor, Product, Quantity |
| 5 | `Price Table` | Central calculation sheet — uses `INDEX/MATCH` (or `VLOOKUP`) to look up Input Price & Coefficients by Product/Distributor, then calculates: `Selling Price`, `Revenue`, `Profit` for each transaction |
| 6 | `Price Table (Filtered)` | "Unpivoted" data table (splits Year/Month, merges Quantity & Revenue into one `Qty & Rev` / `Value` column) — source for the PivotTables |
| 7 | `PT1` | PivotTable: Revenue by **Year → Month** × **Distributor** |
| 8 | `PT2` | PivotTable: Revenue share (%) by Year × Distributor |
| 9 | `PT3` | PivotTable: Revenue by **Year** × **Region** |
| 10 | `PT4 - Top3` | PivotTable: Top 3 best-selling products by Quantity, per Distributor |
| 11 | `PT4 - Top3 (All)` | Extended version of PT4, broken down by Year |
| 12 | `Card` | Overall KPI metrics: Profit, Revenue, Profit Margin, AOV (Average Order Value) |
| 13 | `Qty Filter` | Supporting table for the Quantity slicer |
| 14 | `Dashboard` | **Performance control panel** — combines charts + interactive slicers for the 2022–2024 period |

## 3. Key Formulas & Techniques

- **Data lookup:** `INDEX/MATCH` or `VLOOKUP` to retrieve Input Price (by Product) and Cost/Profit Coefficients (by Distributor + Product Group) from the reference tables.
- **Price & revenue calculation formulas** (sheet `Price Table`):
  - `Selling Price = Input Price / (1 − Sales Cost Coefficient − Profit Coefficient)`
  - `Revenue = Quantity × Selling Price`
  - `Profit = Revenue × Profit Coefficient`
- **PivotTable & Slicer:** multi-dimensional data aggregation (Year/Month/Region/Distributor/Product), interactive filtering on the Dashboard.
- **Charts:** visualize revenue trends, regional and distributor composition, and top products.
- **KPI Cards:** Total revenue, total profit, profit margin, AOV — updated dynamically based on filters.

## 4. Key Business Metrics (Full Period 2022–2024)

| Metric | Value |
|---|---|
| Total Revenue | ~794,042 million VND |
| Total Profit | ~23,544 million VND |
| Profit Margin | ~13.16% |
| Average Order Value (AOV) | ~8.56 million VND |
| Highest-Contributing Region | Southern Region |
| Revenue Growth | Steady year-over-year growth from 2022 to 2024 |

*(Figures sourced from sheets `Card`, `PT1`, `PT3` — unit: million VND)*

## 5. How to Use This File

1. Open the **`Dashboard`** sheet for a visual overview.
2. Use the **Slicers** (Year, Region, Distributor...) to filter data as needed — charts and KPI cards will update automatically.
3. To view the raw calculation data: go to the `Price Table` or `Data` sheet.
4. To check the price/coefficient lookup formulas: see the `Input Price`, `Coefficient`, and `Price` sheets.
5. PivotTables (`PT1`–`PT4`) can be refreshed (right-click → Refresh) if the source data changes.

## 6. Tools Used

Microsoft Excel: Formulas (INDEX/MATCH), PivotTable, PivotChart, Slicer, Conditional Formatting, Dashboard design.
