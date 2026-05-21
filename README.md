# ⚡ EV Charging Station Analytics Dashboard


An end-to-end data analytics project mapping EV charging infrastructure performance, revenue generation, and user behavioral patterns. This project demonstrates full-stack analytics capabilities using SQL for data extraction, Python for Exploratory Data Analysis (EDA), and Power BI for dynamic executive dashboarding.



# 🚀 Project Overview & Core Architecture


The goal of this project is to optimize charging grid load efficiency, track corporate financial targets, and analyze vehicle-specific performance patterns.

The pipeline is split into three core modules:


- Data Extraction & Logic Definition (SQL)

- Exploratory Analysis & Profiling (Python)

- Advanced Visual Analytics & KPI Tracking (Power BI)



# 🛢️ Phase 1: Data Extraction & Analysis (SQL Queries)


The raw transactional data was initially queried and processed via SQL to simulate production-level database management.



## 1. Total Financial Yield & Energy Disbursed


```sql
SELECT 
    ROUND(SUM(Total_Cost_INR), 2) AS Total_Revenue_INR,
    ROUND(SUM(Energy_Consumed_kWh), 2) AS Total_Energy_Disbursed_kWh
FROM EV_Charging_Transactions;
```



## 2. Identifying Peak Infrastructure Load Windows


```sql
SELECT 
    CASE 
        WHEN CAST(Start_Time AS TIME) BETWEEN '08:00:00' AND '18:00:00' THEN 'Peak Hours'
        ELSE 'Off-Peak Hours'
    END AS Time_Slot,
    SUM(Total_Cost_INR) AS Sectional_Revenue
FROM EV_Charging_Transactions
GROUP BY 1;
```



# 🐍 Phase 2: Exploratory Data Analysis (Python)


Before visualization, a Python script was executed to inspect schema constraints, manage data types, and understand initial distribution mechanics.



```python
import pandas as pd

df = pd.read_csv("EV_Charging_Station_Data.csv")

print(df.info())
print(df.describe())

df['Charging_Speed_KWh_Min'] = (
    df['Energy_Consumed_kWh'] / df['Charging_Duration_Mins']
)
```



# 📊 Phase 3: Power BI Business Intelligence & DAX Engineering


The dynamic report features an Executive Overview (Page 1) and Infrastructure Performance (Page 2) tailored for stakeholders.



## 🧠 Core DAX / Custom Metrics Created


```dax
Time_Slot = 
IF(
    HOUR(Sheet1[Start_Time]) >= 8 &&
    HOUR(Sheet1[Start_Time]) <= 18,
    "Peak Hours",
    "Off-Peak Hours"
)
```



```dax
Charging_Speed_KWh_Min = 
DIVIDE(
    Sheet1[Energy_Consumed_kWh],
    Sheet1[Charging_Duration_Mins],
    0
)
```



# 🎯 Business KPIs Tracked


- Revenue Performance: Achieved ₹839.05K against a corporate target of ₹1M (84.2% Target Completion).

- Grid Energy Load Tracker: Disbursed 45.27K KWh against a supply threshold target of 50K KWh (90.7% Efficiency Maintained).

- Infrastructure Optimization: Identified that DC Ultra-Fast Chargers pull the highest revenue chunk (58.4%), while peak charging hours (8 AM - 6 PM) dominate grid dependency at 65.43%.



# 💡 Strategic Insights & Takeaways


## Infrastructure Scaling


Since DC Ultra-Fast chargers drive close to 60% of total revenue, future CAPEX should prioritize high-kilowatt fast dispensers over standard AC Slow chargers.



## Grid Demand Response


65.43% of load hits during the day (Peak Hours). Implementing dynamic time-of-use pricing models during these hours could safely distribute grid pressure to off-peak slots.



## Vehicle Segmentation


4-Wheeler segments (SUVs/Sedans) are the highest energy consumers, calling for strategically placed wide-bay charging stations in high-density corridors.
