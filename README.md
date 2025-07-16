
# 💼 Finance Analysis of AtliQ Hardwares

This project performs a **Profit & Loss (P&L) analysis by Year and Month** using Excel's Power Query and Power Pivot features. Data modeling and visualization are done for a fictional company called AtliQ Hardwares.

---

## 📁 Data Model

The Excel file contains the following data tables:

- `fact_sales_monthly`
- `dim_customer`
- `dim_product`
- `dim_market`
- `dim_date`
- `ns_targets_2021`

---

## 🔄 Power Query Steps

### 1. Import & Prepare Data

- Import `fact_sales_monthly_with_cost.csv`
- Rename the table to: `finance ref`
- Create a **reference** of `finance ref` and rename it: `fact_sales_monthly_with_cost`
- Remove unnecessary transformation steps for clean queries

### 2. Organize Queries

- Group as **Dimension**:
  - `dim_customer`
  - `dim_product`
  - `dim_market`
  - `dim_date`
- Group as **Fact**:
  - `fact_sales_monthly_with_cost`
  - `ns_targets_2021`

### 3. Load Options

- Use "Close & Load to" and keep **"Add to Data Model" unchecked**, as relationships already exist.

---

## 🧮 Power Pivot Calculations

### ➕ Add New Column: COGS

In `fact_sales_monthly_with_cost`:
```excel
= [freight_cost] + [manufacture_cost]
```

### 📏 Create Measures

```excel
Total_net_sales = SUM([net_sales_amount])
COGS = SUM([total_COGS])
Gross Margin = [total_net_sales] – [COGS]
GM % = DIVIDE([gross_margin], [total_net_sales], 0)
```
> Format `GM %` as **Percentage**

---

## 📊 Create P&L by Year Report (Pivot Table)

1. Add `fiscal_year` to **Columns**
2. Add measures to **Values**:
   - `Net Sales`
   - `COGS`
   - `Gross Margin`
   - `GM %`
3. Drag `Measure Values` to **Rows**

### 🆚 Year-on-Year Comparison (Excel Formula)
In Excel:
```excel
=IFERROR((E10 – D10) / D10, "")
```

Apply to all rows to compute `2021 vs 2020`.

---

## ✨ Formatting & Visualization

- Apply **Conditional Formatting**:
  - Use Color Scale for metrics
  - Add **Data Bars** to comparison columns

---

# 📅 P&L by Month Report

## 📋 Report Setup

- Duplicate: `P&L_by_Year` → `P&L_by_Month`

---

## 🧮 Add Time Intelligence Columns (Power Pivot)

### Month Column
```excel
= FORMAT([date], "MMM")
```

### Fiscal Month Number
```excel
= MONTH(DATE(YEAR([date]), MONTH([date]) + 4, 1))
```

### Quarter Column
```excel
= "Q"&ROUNDUP(dim_date[fy_month_no]/3,0)
```

### 🔃 Sort Month
- Sort `Month` by `fy_month_no`

---

## 📊 Configure Pivot Table (Month View)

- Add `fiscal_year` to **Filters**
- Add `Quarter` and then `Month` to **Columns**

### Create Year-Specific Views

1. Filter to 2019, then duplicate for:
   - 2020
   - 2021

---

## 📈 YoY Comparison (Excel Formulas)

```excel
2021 vs 2020: = (C39 - C25) / C25
2020 vs 2019: = (C25 - C11) / C11
```
> Format results as **Percentage**

---

## ✅ Grand Totals

- Enable Grand Totals for full-month metrics summary

---

## 🎨 Visual Enhancements

- Use **3-color scale** for:
  - Metric rows
  - GM % rows
  - YoY comparison rows

Use Format Painter to copy conditional formatting styles.

---

## 📎 Project Folder Structure Suggestion

```plaintext
Finance Analytics/
├── Data/
│   ├── fact_sales_monthly_with_cost.csv
├── Excel/
│   ├── Finance_Analysis_AtliQ.xlsx
├── README.md
```

---

## 🚀 Tools Used

- Microsoft Excel
  - Power Query
  - Power Pivot
  - Pivot Tables
  - Conditional Formatting

---

## 📌 Author

**Nihala R I**  
_MSc Data Science & Analytics_  
_Data Scientist at Softroniics, Calicut_

##  Acknowledgements

This project is based on the Excel Finance Analytics case study taught in the [Codebasics YouTube channel](https://www.youtube.com/@codebasics).  
All modeling, pivot configuration, and formatting were independently implemented by me.
