# 🛍️ Retail Sales Analytics Dashboard

An end-to-end retail sales analytics solution built in **Power BI**, using **Power Query** for data transformation and **DAX** for advanced calculations. The dashboard delivers actionable insights into sales performance, product trends, regional distribution, and customer behavior.

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=flat&logo=microsoftexcel&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=flat&logo=microsoft&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green.svg)

---

## 📊 Overview

This project analyzes retail sales data to help stakeholders track revenue, profit, and growth across products, regions, and time periods. It demonstrates a complete BI workflow — from raw data ingestion to a polished, interactive dashboard.

**Key objectives:**
- Consolidate and clean multi-source retail sales data
- Build a robust star-schema data model
- Create reusable DAX measures for KPIs and trend analysis
- Design an interactive, decision-ready dashboard

---

## ✨ Features

- **Sales Overview** — total revenue, profit, quantity sold, and YoY/MoM growth
- **Product Analysis** — top/bottom performing products and categories
- **Regional Performance** — sales distribution by region/state with map visuals
- **Time Intelligence** — trend analysis using DAX time-intelligence functions (YTD, QTD, MTD, prior period comparisons)
- **Customer Segmentation** — RFM-style breakdown of customer value
- **Dynamic Filtering** — slicers for date range, category, region, and channel
- **Drill-through pages** for product- and region-level deep dives

---

## 🗂️ Project Structure

```
retail-sales-analytics-dashboard/
│
├── README.md                          # Project documentation (this file)
├── LICENSE
├── .gitignore
│
├── data/
│   └── sample_retail_sales.csv        # Sample dataset for demo/testing
│
├── power-query/
│   └── data_transformation_steps.md   # M code / ETL transformation steps
│
├── dax/
│   └── measures.md                    # Core DAX measures used in the model
│
├── docs/
│   ├── data_model.md                  # Star schema documentation
│   └── screenshots/                   # Dashboard screenshots (add your own)
│
└── RetailSalesAnalyticsDashboard.pbix # Power BI file (add your own — see note below)
```

> **Note:** The `.pbix` file itself is a binary Power BI file authored in Desktop. Add your own exported `.pbix` to the repo root before pushing — GitHub will store it via Git LFS recommended for files over ~50MB (see `.gitignore` / LFS note below).

---

## 🧱 Data Model

The report uses a **star schema** for optimal performance:

| Table | Type | Description |
|---|---|---|
| `FactSales` | Fact | Transaction-level sales records (date, product, region, quantity, revenue, cost) |
| `DimDate` | Dimension | Continuous calendar table with year/quarter/month hierarchies |
| `DimProduct` | Dimension | Product name, category, sub-category |
| `DimRegion` | Dimension | Region/state/city hierarchy |
| `DimCustomer` | Dimension | Customer ID, segment |

See [`docs/data_model.md`](docs/data_model.md) for the full relationship diagram.

---

## 🔧 Power Query (ETL)

Data is cleaned and shaped using Power Query before loading into the model:

- Removed duplicates and null transactions
- Standardized date formats and created a continuous `DimDate` table
- Split/merged category-subcategory columns
- Unpivoted monthly columns for a normalized fact table
- Applied conditional columns for profit margin buckets

Full M code steps: [`power-query/data_transformation_steps.md`](power-query/data_transformation_steps.md)

---

## 📐 Key DAX Measures

```dax
Total Revenue = SUM(FactSales[SalesAmount])

Total Profit = SUM(FactSales[Profit])

Profit Margin % = DIVIDE([Total Profit], [Total Revenue], 0)

Sales YTD = TOTALYTD([Total Revenue], DimDate[Date])

Sales PY = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR(DimDate[Date]))

Sales YoY Growth % = DIVIDE([Total Revenue] - [Sales PY], [Sales PY], 0)
```

Full measure list with explanations: [`dax/measures.md`](dax/measures.md)

---

## 🚀 Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/retail-sales-analytics-dashboard.git
   ```
2. Open `RetailSalesAnalyticsDashboard.pbix` in **Power BI Desktop** (2023+ recommended).
3. Update the data source path in **Power Query Editor** to point to `data/sample_retail_sales.csv` (or your own source).
4. Click **Refresh** to load the data.
5. Explore the report pages via the navigation tabs.

---

## 🖼️ Screenshots

> Add exported screenshots of your report pages to `docs/screenshots/` and reference them here, e.g.:
>
> `![Sales Overview](docs/screenshots/sales-overview.png)`

---

## 🛠️ Tools & Technologies

- **Power BI Desktop** — report authoring and visualization
- **Power Query (M)** — data extraction, cleaning, and transformation
- **DAX** — calculated columns, measures, and time intelligence
- **Data Modeling** — star schema design

---

## 📈 Sample Insights (edit with your findings)

- Identified top 5 revenue-driving product categories
- Found a X% YoY growth in Q4 sales
- Flagged underperforming regions for targeted promotions
- Highlighted seasonal demand spikes to inform inventory planning

---

## 📄 License

This project is licensed under the MIT License — see [`LICENSE`](LICENSE) for details.

---

## 🙋 Author

**Your Name**
[LinkedIn](#) • [Portfolio](#) • [Email](#)
