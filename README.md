# 📊 Sales Analysis

## 📌 Project Overview

This project analyzes **BrightMart Inc.'s sales data from 2014 to 2018** to understand revenue and profit performance, seasonality, product and channel performance, regional and state trends, customer behavior, and pricing patterns.

The project uses **Python for Exploratory Data Analysis (EDA)**, **Power BI for interactive visualization**, and a **PowerPoint presentation** to communicate the major business findings and recommendations in plain English.

> **Goal:** find out which products, channels and markets drive revenue and profit, spot seasonality and outliers, and turn the findings into practical actions on pricing, promotions and growth.

---

## 🎯 Business Objectives

The main objectives of this project are to:

- Analyze overall revenue, profit and profit margin.
- Identify seasonal patterns and unusual months.
- Find the best and weakest products by revenue and margin.
- Compare sales channels (Wholesale, Distributor, Export).
- Understand how unit price relates to revenue and margin.
- Compare regions and states to find growth opportunities.
- Identify top and bottom customers and check revenue concentration.
- Present the findings through an interactive Power BI dashboard.
- Recommend actions on pricing, promotions, market expansion and diversification.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Python** (pandas, NumPy) | Data loading, cleaning, merging and feature creation |
| **Matplotlib / Seaborn / Plotly** | Exploratory charts and the state map |
| **Jupyter Notebook** | EDA workflow and written insights |
| **Power BI** (Power Query, DAX) | Data model, measures and interactive dashboard |
| **Microsoft PowerPoint** | Business presentation and recommendations |
| **Excel / CSV** | Source workbook and cleaned export |

---

## 📂 Dataset

The source is a regional sales workbook, `Regional Sales Dataset.xlsx` (not included in this repo), with six sheets:

`Sales Orders` · `Customers` · `Products` · `Regions` · `State Regions` · `2017 Budgets`

After cleaning, the final table contains **64,104 order lines** covering **January 2014 to February 2018**, with **175 customers**, **30 products**, **47 states** and **3 sales channels**.

### Important Columns in the Final Data

- `order_number`, `order_date`
- `customer_name`, `channel`, `product_name`
- `quantity`, `unit_price`, `revenue`, `cost`
- `state`, `state_name`, `us_region`, `lat`, `lon`
- `budget` (2017 only)
- `total_cost`, `profit`, `profit_margin_pct`
- `order_month`, `order_month_name`, `order_month_num`

---

## 🐍 Step 1: Python EDA (`EDA.ipynb`)

### 🔹 Setup & Loading
1. Defined the problem statement.
2. Imported pandas, NumPy, Matplotlib, Seaborn (and Plotly for the map).
3. Read all sheets of the workbook and assigned each to its own dataframe.

### 🔹 Data Understanding
4. Checked the shape of every table and previewed the first rows.
5. Fixed the State Regions sheet by promoting its first row to the header.
6. Checked every table for missing values.

### 🔹 Data Cleaning & Wrangling
7. Merged the tables step by step (left joins):
   `Sales Orders` → `+ Customers` → `+ Products` → `+ Regions` → `+ State Regions` → `+ 2017 Budgets`
8. Dropped duplicate key columns left over from the merges.
9. Converted column names to lowercase, kept only the useful columns and renamed them to clean snake_case.
10. Blanked out the budget column for non-2017 orders.
11. Re-checked data types and missing values.

### 🔹 Feature Engineering
- `total_cost` = quantity × unit cost
- `profit` = revenue − total cost
- `profit_margin_pct` = profit ÷ revenue × 100
- Month, month name and month number for the seasonality charts

### 🔹 Exploratory Analysis (15 sections)

| # | Analysis |
|---|---|
| 1 | Monthly sales trend over time |
| 2 | Monthly sales trend, all years combined |
| 3 | Top 10 products by revenue |
| 4–5 | Sales by channel (including pie chart) |
| 6 | Order value distribution |
| 7 | Profit margin % vs unit price |
| 8 | Unit price distribution per product (box plot) |
| 9 | Total sales by US region |
| 10 | Total sales by state (choropleth map) |
| 11 | Top 10 states by revenue and order count |
| 12 | Average profit margin by channel |
| 13 | Top and bottom 10 customers by revenue |
| 14 | Customer segmentation: revenue vs profit margin |
| 15 | Correlation heatmap of numeric features |

Each section has a short written insight underneath it.

### 🔹 Export
- Exported the cleaned dataframe (`Sales_data (EDA Exported)`) to use as the Power BI data source.

---

## 📈 Step 2: Power BI Dashboard (`REPORT.pbix`)

### 🔹 Load & Prepare (Power Query)
1. Imported the exported file as the `Sales_data` table.
2. Promoted headers and set the correct data types.
3. Added a `year` column from the order date.

### 🔹 Data Model (DAX)
4. **`Customer Summary`** table: one row per customer with Total Revenue, Total Profit, Avg Profit Margin % and Order Count.
5. **`Order_Value_Distribution`** table: one row per order with its total value.
6. **Bin columns** (`revenue (bins)`, `OrderValue (bins)`) to group orders into spending tiers.
7. **`Measures_`** table with the key measures:
   `Total Revenue` · `Total Profit` · `Profit Margin %` · `Total Orders` · `Revenue per order` · `Top State by Revenue` · `Top State Revenue` · `Top State by Profit Margin` · `States >5% Revenue`

### 🔹 Dashboard Pages

**1️⃣ Executive Overview & Trends**
- KPI cards: Total Revenue, Total Profit, Profit Margin %, Total Orders, Revenue per order
- Monthly Revenue Rhythm
- Tracking Monthly Earnings Momentum
- Unit Price vs Profit Margin
- Mapping Customer Spending Tiers

**2️⃣ Product & Channel Performance**
- Best-Selling Products Driving Growth
- Most Efficient Products to Sell
- Revenue vs. Profitability (by customer)
- Channel Power Play, Profit Pipeline by Channel, Channel Efficiency Scorecard

**3️⃣ Geographic & Customer Insights**
- Top 5 / Bottom 5 Customers by Revenue
- Top 5 / Bottom 5 Customers by Profit Margin
- Top 5 / Bottom 5 States by Revenue
- Profit by State (map)
- Total Revenue by Region and Profit Margin % by Region

### 🔹 Interactivity & Design
- Slicers for **year, month, US region and channel** on every page
- **Clear all slicers** button and a filter-panel button
- Page navigation buttons and **Top 5 / Bottom 5** toggle buttons (bookmarks)

### 🖼️ Dashboard Preview

```text
images/Dashboard.png
```
![Sales Analysis Dashboard]
<img width="1428" height="801" alt="1st" src="https://github.com/user-attachments/assets/ca21a8f8-aaa6-4036-80d4-08e11322dc66" />
<img width="1432" height="797" alt="2nd" src="https://github.com/user-attachments/assets/795d467c-5394-45aa-a8b5-0c76beba5add" />
<img width="1432" height="798" alt="3rd" src="https://github.com/user-attachments/assets/46071670-b861-4584-be9f-e52289d4bd95" />

---

## 📊 Key Findings

| Metric | Value |
|---|---|
| 💰 Total revenue | **$1.24B** |
| 📈 Total profit | **$462M** |
| 🎯 Profit margin | **37.4%** |
| 📅 Average monthly revenue | about **$24.7M** |

### 🔍 What the data shows

- **Steady, not growing.** Yearly revenue is almost flat (about $294M to $298M for 2014–2017). February 2017 is a clear dip at $21.2M.
- **February is the quietest month;** May and August are the strongest, but the gap is only about 12%.
- **Two products lead.** Products 26 and 25 bring in about 18% of revenue, and 11 of 30 products each sell under $20M.
- **Margins are tightly packed** (about 34–40% across products), so volume decides which products win.
- **Wholesale is 54% of revenue.** Export is the smallest channel (about 15%) but has the best margin (38.0%).
- **Price does not predict margin** (correlation about zero), but it does drive revenue (about 0.91).
- **The West leads (about 30%); the Northeast lags (about 17%)** at the same margins.
- **California is about 18.5% of revenue,** and California, Illinois, Florida and Texas together earn about 42% of profit.
- **No customer is a big risk:** the ten largest are only about 9% of revenue across 175 customers.

---

## 💡 Recommendations

1. 🌍 **Grow Export** — smallest channel with the best margin.
2. 📍 **Close the Northeast gap** with local promotions and partnerships.
3. 🗓️ **Plan around February** and investigate what happened in February 2017.
4. 🏷️ **Review margin line by line** — discounts for low-margin customers and the low-revenue products.

---

## 📑 Step 3: Business Presentation

`BrightMart_Dashboard_Review.pptx` recreates the dashboard charts from the report's data, with a plain-English takeaway and speaker notes on every slide. All charts are native and editable.

---

## 📁 Project Structure

```text
Sales-Analysis/
│
├── Dataset/
│   └── Regional Sales Dataset.xlsx
│
├── Python_EDA/
│   └── EDA.ipynb
│
├── PowerBI/
│   └── REPORT.pbix
│
├── PPT/
│   └── BrightMart_Dashboard_Review.pptx![Uploading 2nd.png…]()
│
└── README.md
```

---

## 📌 Project Workflow

```text
Regional Sales Dataset (6 sheets)
        ↓
Python: Load, Clean & Merge
        ↓
Feature Engineering (profit, margin, dates)
        ↓
Exploratory Data Analysis (15 sections)
        ↓
Export Cleaned Data
        ↓
Power BI: Data Model, DAX & Dashboard
        ↓
Business Presentation
        ↓
Recommendations
```

---

## ⚠️ Notes & Limitations

- **2018 is partial.** Data stops after February 2018, so year comparisons use 2014–2017.
- **"Total Orders" counts order lines.** The dashboard measure counts rows (64,104), while there are 10,684 distinct orders. So the dashboard's Revenue per order (about $19K) is per order line; per distinct order it is about $116K.
- **Budget vs actual is not covered.** The 2017 budget field is stored as text and needs cleaning before a fair comparison.
- **Some notebook insight sentences differ from the dashboard data** (for example the January trough and some regional percentages). The dashboard and presentation use the figures from the Power BI data model.

---

## 🚀 How to Run

**Notebook**
```bash
pip install pandas numpy matplotlib seaborn plotly openpyxl jupyter
jupyter notebook Python_EDA/EDA.ipynb
```
Place `Regional Sales Dataset.xlsx` in the `Dataset/` folder and update the file path in the loading cell.

**Dashboard:** open `REPORT.pbix` in [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (Windows). If the data path has changed, update it under *Transform data → Source*.

**Presentation:** open the `.pptx` in PowerPoint, Keynote or Google Slides.

---

## 👨‍💻 Skills Demonstrated

- Python (pandas, NumPy)
- Data Cleaning & Wrangling
- Exploratory Data Analysis
- Feature Engineering
- Power BI & DAX
- Data Visualization
- KPI & Revenue Analysis
- Customer & Regional Analysis
- Business Problem Solving
- Data Storytelling
- Presentation Skills

---

## ⭐ Conclusion

The **Sales Analysis** project shows how raw regional sales data can be turned into clear business insights using **Python, Power BI and PowerPoint**.

The EDA explains what is happening in the data, the Power BI dashboard lets anyone explore it by year, month, region and channel, and the presentation turns it into simple recommendations: grow Export, close the Northeast gap, plan around February, and review margins line by line.

---

## 👤 Author

**Your Name** · [LinkedIn](https://www.linkedin.com/in/aditya-pradhan-85677b34a/) 
