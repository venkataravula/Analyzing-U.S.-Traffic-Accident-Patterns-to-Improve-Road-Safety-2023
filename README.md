# Analyzing-U.S.-Traffic-Accident-Patterns-to-Improve-Road-Safety-2023
A Data Analyst project using MySQL, Python, Power BI, and Azure to explore and visualize U.S. traffic accident data from the FARS (Fatality Analysis Reporting System) dataset. Focused on ETL, EDA, and end-to-end dashboard reporting.

# 🚗 U.S. Traffic Accident Analysis – FARS Project

This project analyzes traffic accident data from the Fatality Analysis Reporting System (FARS) using SQL, Python, and Power BI. It demonstrates end-to-end data analytics skills including:

- ✅ Data modeling & cleaning (ETL)
- ✅ SQL querying & insights
- ✅ Python-based exploratory data analysis (EDA)
- ✅ Power BI dashboard creation
- ✅ Cloud storage integration with Microsoft Azure
- ✅ Full documentation and visualization

## 🔧 Tools & Technologies

- MySQL (Data storage and SQL analysis)
- Python (Pandas, Seaborn, Matplotlib, SQLAlchemy)
- Power BI (Interactive dashboard visualization)
- Azure Blob Storage (Cloud data hosting)
- Git & GitHub (Version control and documentation)

## 📁 Dataset Source

Data comes from the [National Highway Traffic Safety Administration (NHTSA)](https://www.nhtsa.gov/research-data/fatality-analysis-reporting-system-fars).

| **Purpose**                     | **Suggested File Name**                  |
| ------------------------------- | ---------------------------------------- |
| Python notebook for SQL + EDA   | `sql_eda.ipynb`        |
| SQL queries only                | `sql_queries.py` or `exploratory_sql.py` |
| Data cleaning (Python)          | `data_cleaning.py`                       |
| Visualization script            | `visualizations.py`                      |
| Combined script (ETL + EDA)     | `fars_analysis.py` or `fars_pipeline.py` |
| Power BI export prep (optional) | `export_for_powerbi.py`                  |


## 🧮 SQL Analysis (Week 2, Day 3–5)

I performed SQL-based exploration on MySQL using data from NHTSA’s FARS dataset.

### 🔍 Key Questions

- States with highest fatalities
- Peak accident hours
- Average driver age in fatal crashes

### 📊 Sample Query – Fatalities by State

```sql
SELECT statename, SUM(fatals) AS total_fatalities
FROM accident
GROUP BY statename
ORDER BY total_fatalities DESC
LIMIT 10;
✅ This helped us identify that states like Texas and California had the most accident-related deaths.****
