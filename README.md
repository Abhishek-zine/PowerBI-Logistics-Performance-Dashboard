# 🚛 Power BI Logistics Performance Dashboard

### 🎯 Objective
To design an **interactive Power BI dashboard** for analyzing **carrier performance, delay reasons, and load efficiency** across logistics operations — improving visibility, reducing delays, and enabling data-driven decisions.

---

## 🧩 Project Overview
This project combines **SQL**, **Power Query (M)**, and **DAX modeling** to build a real-time logistics performance dashboard.

**Key Insights Delivered:**
- Total and delayed loads
- On-time performance trends
- Carrier reliability ranking
- Delay reason analysis by office, date, and agent
- Customer-level performance insights

---

## ⚙️ Data Source
Three tables were used from SQL Server:

| Table | Description |
|--------|--------------|
| `ALX_OFF_LOGS_HIST` | Log details (creation date, delay reasons, status) |
| `ALX_OFF_CARRIERS_HIST` | Carrier/vendor data |
| `ALX_OFF_LOAD_HISTORY_INFO_HIST` | Load, customer, and office data |

**SQL Query:**
```sql
Select Distinct 
 L.EFJ_HEADER_ID,
 L.Log_ID,
 Convert(Date,L.Creation_Date) as Creation_Date_Only,
 L.Creation_Date,
 L.REASONS_FOR_DELAY,
 L.STATUS_ID,
 L.Comments,
 Left(L.Comments,charindex(' ',L.Comments)-1) as Comments_Carrier_Number_Uncovered,
 C.Vendor_Name as Vendor_Name_Uncovered,
 Carrier_Num,
 I.Load_ID,
 I.Customer_Name,
 I.Customer_Number,
 I.Actual_PU_Date,
 I.Load_Manager,
 I.Carrier_Entry,
 I.Office,
 I.Covered_By,
 I.Covered_By_Office
From alctms.ALX_OFF_LOGS_HIST L
Left Join alctms.ALX_OFF_CARRIERS_HIST C on C.Carrier_Num = Left(L.Comments,charindex(' ',L.Comments)-1)
Left Join alctms.ALX_OFF_LOAD_HISTORY_INFO_HIST I on L.EFJ_HEADER_ID = I.EFJ_HEADER_ID
Where L.STATUS_ID = '21'
and Convert(Date,L.Creation_Date) > '2024-12-31'
