# Amazon Store Sales Dashboard – README

## 1. Project Overview
This **Power BI** report presents a one‑page interactive dashboard that helps stakeholders quickly grasp *what is selling, where it sells, and how profitable it is* across Amazon’s retail catalogue. The focus is on:

- **Revenue & Profitability** – headline metrics for total sales and profit (₹).
- **Product Mix** – performance sliced by *Segment, Category, Sub‑Category* and individual *Products*.
- **Geography** – sales heat‑mapped down to the U.S. *State* level and filterable by *Region*.
- **Time** – month‑over‑month trends with drill‑down to individual order dates.
- **Returns** – the ratio of shipped orders that were subsequently returned.

Designed for busy managers, the layout balances at‑a‑glance KPI cards with deeper drill‑down visuals that answer the who/what/where/when of Amazon store performance.

--- --<img src="Amazon_Dashboard.png" height=600px width="1250px">-

## 2. File Inventory
| File | Purpose |
|------|---------|
| **Amazon store sales dashboard.pbix** | Main Power BI Desktop file containing data model, measures, and report layout |
| **Amazon Store Sales Data.xlsx** (imported) | Source data for Orders, Products, and Geography tables |

> **Tip:** Keep the Excel file in the same folder as the PBIX or update the *Data Source Settings* after moving it.

---

## 3. Data Model
The report uses a *single‑table* star schema imported from **Sheet1** of the Excel data file. Key columns include:

- `Order ID` (Guid / Text)
- `Order Date` (Date – supports built‑in *Date Hierarchy*)
- `Region`, `State` (Geography hierarchy)
- `Segment` (Consumer, Corporate, Home Office)
- `Category`, `Sub-Category`, `Product Name`
- `Product ID`
- `Sales` (₹, decimal)
- `Profit` (₹, decimal)
- `Return Status` (Returned / Not Returned)

Calculated measures (in **DAX**) include but are not limited to:

```DAX
Total Sales = SUM('Sales Data'[Sales])
Total Profit = SUM('Sales Data'[Profit])
Profit Margin % = DIVIDE([Total Profit], [Total Sales])
Returned Orders = CALCULATE(COUNTROWS('Sales Data'), 'Sales Data'[Return Status] = "Returned")
Return Rate % = DIVIDE([Returned Orders], DISTINCTCOUNT('Sales Data'[Order ID]))
```

Feel free to extend the model (e.g. add a *Date* dimension for Y-over-Y calculations) using **Model view > New Table**.

---

## 4. Report Canvas & Visual Catalog
All visuals reside on **Page 1 • Sales Overview**. The grid is arranged left‑to‑right, top‑to‑bottom for natural scanning:

| # | Visual | Fields | Insight |
|---|--------|--------|---------|
|1| **KPI Card – Total Sales** | *Total Sales* | Headline revenue |
|2| **KPI Card – Total Profit** | *Total Profit* | Overall profitability |
|3| **KPI Card – Distinct Products** | *DISTINCTCOUNT(Product ID)* | Catalogue breadth |
|4| **KPI Card – Distinct Orders** | *DISTINCTCOUNT(Order ID)* | Order volume |
|5| **Donut Chart – Sales by Segment** | *Segment*, *Total Sales* | Which customer segments drive revenue |
|6| **Area Chart – Monthly Sales Trend** | *Month > Year*, *Total Sales* | Seasonality & YoY comparison |
|7| **Clustered Column – Quarterly Profit** | *Quarter*, *Total Profit* | Profit fluctuations across quarters |
|8| **Clustered Bar – Sales by Category** | *Category*, *Total Sales* | High-level product category mix |
|9| **Clustered Bar – Profit by Sub-Category** | *Sub-Category*, *Total Profit* | Granular profit drivers |
|10| **Map – Sales by State** | *State*, *Total Sales* | Geographic hotspots |
|11| **Pie Chart – Return Status** | *Return Status*, *Order Count* | Share of orders returned |
|12| **Slicer – Region** | *Region* | Cross-filter all visuals |
|13| **Slicer – State** | *State* | Drill deeper into geography |
|14| **Slicer – Product Name** | *Product Name* | Focus on a single SKU |

Hover tooltips show exact values; clicking a segment acts as a filter across the page thanks to **Edit Interactions** settings.

---

## 5. Refresh & Maintenance
1. **Open** the PBIX in **Power BI Desktop (June 2025 or later)**.
2. Go to **Home > Transform Data > Data Source Settings** to confirm the path to *Amazon Store Sales Data.xlsx*.
3. Click **Home > Refresh** or schedule refresh in the Power BI Service after publishing.
4. If the Excel schema changes (new columns), update **Power Query Editor** and **Relationships** accordingly.

> **Automation tip:** Use *OneDrive/SharePoint* for the Excel file so the PBI Service picks up the latest snapshot automatically.

---

## 6. Extending the Dashboard
- **Add more KPIs** – e.g. *Avg. Order Value*, *Units Sold*.
- **Implement drill-through** to a dedicated *Order Details* page.
- **Enable Q&A** by reviewing column synonyms and data categories.
- **Mobile Layout** – optimize for phones via **View > Mobile Layout**.

---

## 7. Performance Notes
- The dataset is small (< 1 MB); *Import* mode suffices and renders instantly.
- All measures are simple aggregates—no heavy row-context iterations.
- Keep *Auto-date/time* disabled if you introduce a dedicated Calendar table.

---

## 8. Requirements
| Software | Version |
|-----------|---------|
| Windows 10/11 | 64‑bit |
| **Power BI Desktop** | 2.130.901.0 (June 2025) or later |
| Excel (optional) | 2016+ or Microsoft 365 |

---

## 9. Author & Support
**Created by:** *Mihir Limje*  
**Last updated:** 19 July 2025  

For suggestions or issues raise a ticket in the project tracker or email **mihir.limje@example.com**.

---

## 10. License
Distributed under the **MIT License** – see `LICENSE` for details.

> © 2025 Mihir Limje. All rights reserved.
