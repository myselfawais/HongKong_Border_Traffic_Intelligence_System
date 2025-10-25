# 🇭🇰 Hong Kong Border Trafffic Intelligence System (2021–2024)

A full end-to-end **SQL + Power BI** analytics project analyzing Hong Kong's Control Point passenger traffic trends from **2021 to 2024**, covering the pandemic decline, reopening rebound, and post-recovery normalization.

---

## 📊 Project Overview

This project explores how passenger traffic across Hong Kong's 16 control points.
Using **PostgreSQL for data analysis** and **Power BI for visualization**, this dashboard reveals trends in passenger growth, visitor composition, and control point performance.

---

## 🧠 Key Insights

| Category | Insight |
|----------|---------|
| 📅 **Date Range** | Jan 2021 → Dec 2024 (44,328 daily records) |
| 👥 **Total Passengers** | 517 million+ across all crossings |
| 📈 **Growth Trends** | 2023 saw a 3924% YoY rebound after border reopening |
| 🌍 **Visitor Mix** | Hong Kong Residents ~70%, Mainland Visitors ~23%, Others ~7% |
| 🚉 **Top Crossings** | Lo Wu (109M), Lok Ma Chau Spur Line (96M), Airport (78M) |
| ⚖️ **Arrivals vs Departures** | 49.98% arrivals vs 50.02% departures — perfectly balanced |
| 🗓️ **Weekly Patterns** | Highest traffic on weekends (Sat/Sun); lowest midweek (Wed) |

---

## 📊 Power BI Dashboard Features

| Visualization | Purpose |
|---------------|---------|
| **KPI Cards** | Total Passengers, YoY Growth, Top Control Point, HK Resident Share, Peak Month |
| **Line Chart** | Monthly traffic trend (2021–2024) |
| **Bar Chart** | Top 10 busiest control points |
| **Stacked Bar** | Visitor type composition by month |
| **Pie Chart** | Visitor distribution (%) |
| **Column Chart** | Arrivals vs Departures |
| **Line + Marker Chart** | YoY growth trend |
| **Matrix Heatmap** | Weekday traffic patterns |

---

## 🧩 Data Sources

-Statistics on Passenger Traffic of Hong Kong
from Immigration of HKSAR

---

## 🧮 SQL Analysis

All SQL queries used in this project are available in the Queries folder.

### Example: Year-over-Year Growth
```sql
SELECT
    EXTRACT(YEAR FROM date) AS year,
    SUM(total_passengers) AS total_passengers,
    ROUND(
        (SUM(total_passengers) - LAG(SUM(total_passengers)) OVER (ORDER BY EXTRACT(YEAR FROM date))) 
        / LAG(SUM(total_passengers)) OVER (ORDER BY EXTRACT(YEAR FROM date)) * 100, 2
    ) AS yoy_growth_percentage
FROM border_traffic
GROUP BY EXTRACT(YEAR FROM date)
ORDER BY year;
```

## ⚙️ Tools & Technologies

| Tool | Purpose |
| :--- | :--- |
| **PostgreSQL** | Data storage, SQL querying & aggregation |
| **Power BI** | Dashboard creation & visualization |
| **Excel / Power Query** | Data cleaning & transformation |

## 🧠 Learnings & Skills Demonstrated

- **Advanced SQL Aggregation** - CTEs, window functions, and date functions
- **Data Modeling & Transformation** - Preparing data for BI tools
- **Power BI Design** - Visual hierarchy and layout design principles
- **DAX Calculations** - Creating KPIs, calculated measures, and YoY comparisons
- **Data Storytelling** - Building interactive dashboards for insights
- **Project Management** - Github Documentation

## 🚀 How to View the Dashboard

1. **Download** the `.pbix` file from the `/PowerBi_Dashboard` directory
2. **Open** the file in Power BI Desktop (latest version)
3. **Explore** using the interactive filters for year, control point, and visitor 

## 🧾 Author

**Muhammad Awais** 
📍 Data Analyst | SQL | Power BI | Excel | Data Visualization  
🔗 [LinkedIn Profile](https://www.linkedin.com/in/muhammad-awais-40785b346/)  
📧 [contact21rvt@gmail.com]
