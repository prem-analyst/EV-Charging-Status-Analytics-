# ⚡ EV Charging Station Analytics Dashboard

An end-to-end data analytics project mapping EV charging infrastructure performance, revenue generation, and user behavioral patterns. This project demonstrates full-stack analytics capabilities using **SQL** for data extraction, **Python** for Exploratory Data Analysis (EDA), and **Power BI** for dynamic executive dashboarding.

---

## 🚀 Project Overview & Core Architecture

The goal of this project is to optimize charging grid load efficiency, track corporate financial targets, and analyze vehicle-specific performance patterns. 

The pipeline is split into three core modules:
1. **Data Extraction & Logic Definition (SQL)**
2. **Exploratory Analysis & Profiling (Python)**
3. **Advanced Visual Analytics & KPI Tracking (Power BI)**

---

## 🛢️ Phase 1: Data Extraction & Analysis (SQL Queries)

*The raw transactional data was initially queried and processed via SQL to simulate production-level database management.*

### 1. Total Financial Yield & Energy Disbursed
```sql
SELECT 
    ROUND(SUM(Total_Cost_INR), 2) AS Total_Revenue_INR,
    ROUND(SUM(Energy_Consumed_kWh), 2) AS Total_Energy_Disbursed_kWh
FROM EV_Charging_Transactions;
SELECT 
    CASE 
        WHEN CAST(Start_Time AS TIME) BETWEEN '08:00:00' AND '18:00:00' THEN 'Peak Hours'
        ELSE 'Off-Peak Hours'
    END AS Time_Slot,
    SUM(Total_Cost_INR) AS Sectional_Revenue
FROM EV_Charging_Transactions
GROUP BY 1;
import pandas as pd

# Loading dataset for diagnostic profiling
df = pd.read_csv("EV_Charging_Station_Data.csv")

# Profiling data structure and checking for system anomalies
print(df.info())
print(df.describe())

# Feature engineering simulation: Verifying core rate columns
df['Charging_Speed_KWh_Min'] = df['Energy_Consumed_kWh'] / df['Charging_Duration_Mins']
Time_Slot = IF(HOUR(Sheet1[Start_Time]) >= 8 && HOUR(Sheet1[Start_Time]) <= 18, "Peak Hours", "Off-Peak Hours")
Charging_Speed_KWh_Min = DIVIDE(Sheet1[Energy_Consumed_kWh], Sheet1[Charging_Duration_Mins], 0)
