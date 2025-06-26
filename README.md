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

### 📊 Sample Query – 

```sql
SELECT statename, SUM(fatals) AS total_fatalities
FROM accident
GROUP BY statename
ORDER BY total_fatalities DESC
LIMIT 10;
✅ This helped us identify that states like Texas and California had the most accident-related deaths.****

Day 5   ## Data Cleaning or ## Preprocessing
🧼 Data Cleaning: person.csv
As part of the ETL process, we performed data cleaning on the person.csv file before importing it into MySQL. The raw CSV file contained many missing (NaN) values, especially in categorical fields. This step was necessary to ensure data integrity and prevent SQL import errors.
import pandas as pd

# Load raw CSV file
df = pd.read_csv("D:/Project/files/person.csv", low_memory=False)

# Replace NaN values only in object (string/categorical) columns
str_cols = df.select_dtypes(include='object').columns
df[str_cols] = df[str_cols].fillna("Unknown")
-=---------------------------------------------------------------------------
##Use Python to Load CSV into MySQL (more reliable)

import pandas as pd
from sqlalchemy import create_engine

# Load cleaned person data
df = pd.read_csv("D:/Project/files/cleaned_vehicle.csv", low_memory=False)

# Connect to MySQL
engine = create_engine("mysql+pymysql://root:root@localhost/fars_traffic_analysis")

# Push to MySQL
df.to_sql("vehicle", con=engine, index=False, if_exists="replace", chunksize=1000)

# Save the cleaned data to a new CSV file
df.to_csv("D:/Project/files/person_cleaned.csv", index=False)
✅ Outcome:
Missing values in text fields are replaced with "Unknown".

Numeric columns remain unchanged to preserve data types.

The cleaned CSV (person_cleaned.csv) is ready for high-performance import into MySQL using LOAD DATA INFILE.

📌 Notes:
This step ensures consistent formatting and avoids common MySQL import errors like:

Incorrect integer value: 'Unknown' for column 'some_column'

Cleaning was performed using pandas for efficient handling of large datasets.
'''
## Verify Data in Python

import pandas as pd
from sqlalchemy import create_engine

engine = create_engine("mysql+pymysql://root:root@localhost/fars_traffic_analysis")

# Count rows
for table in ['accident', 'person', 'vehicle']:
    count = pd.read_sql(f"SELECT COUNT(*) as total FROM {table}", engine)
    print(f"{table}: {count['total'][0]} rows")

```
## 📊 Exploratory Data Analysis (Python)

In this step, we analyze the `accident` table from the FARS Traffic Accident dataset using Python libraries such as **pandas**, **seaborn**, and **matplotlib**. The database connection is established via **SQLAlchemy** to MySQL.


### 🔌 Step 1: Load Data from MySQL

We connect to the MySQL database and read the `accident` table into a pandas DataFrame:

```python
from sqlalchemy import create_engine
import pandas as pd

engine = create_engine("mysql+pymysql://root:root@localhost/fars_traffic_analysis")
df_accident = pd.read_sql("SELECT * FROM accident", engine)


import matplotlib.pyplot as plt

plt.figure(figsize=(10,6))
df_accident.groupby("statename")["fatals"].sum().sort_values(ascending=False).head(10).plot(
    kind="bar", color="salmon", edgecolor="black"
)
plt.title("Top 10 States by Fatalities", fontsize=14)
plt.ylabel("Total Fatalities")
plt.xlabel("State")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()



import seaborn as sns

plt.figure(figsize=(12,6))
order = ['12:00 AM', '1:00 AM', '2:00 AM', ..., '11:00 PM']  # chronological order
sns.countplot(data=df_accident, x="hourname", order=order, palette="crest")
plt.title("Accidents by Hour of the Day", fontsize=14)
plt.xlabel("Hour")
plt.ylabel("Number of Accidents")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()


🧠 Tools Used
Python 3

pandas for data manipulation

matplotlib/seaborn for visualization

SQLAlchemy/pymysql for database connection
