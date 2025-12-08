# 🚛 Power BI Logistics Performance Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=for-the-badge&logo=microsoft-sql-server&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=powerbi&logoColor=white)

An interactive Power BI dashboard for analyzing Walmart carrier performance, delay reasons, and load efficiency across logistics operations — improving visibility, reducing delays, and enabling data-driven decisions.

## 📊 Dashboard Preview

![Dashboard Preview](image%20(2).png)

## 🎯 Objective

To design an **interactive Power BI dashboard** for analyzing **carrier performance, delay reasons, and load efficiency** across logistics operations — improving visibility, reducing delays, and enabling data-driven decisions for Walmart logistics.

## ✨ Key Features

### 📈 Performance Metrics
- **Total Loads & Delayed Loads** tracking
- **On-time Performance Trends** visualization
- **Carrier Reliability Ranking** system
- **Delay Reason Analysis** by office, date, and agent
- **Customer-Level Performance** insights

### 🔍 Interactive Analysis
- Dynamic filtering by date, office, and carrier
- Drill-down capabilities for detailed investigation
- Real-time performance monitoring
- Comparative analysis across carriers and time periods

## 🛠️ Technical Stack

- **Power BI Desktop** - Dashboard development and visualization
- **SQL Server** - Database backend
- **Power Query (M)** - Data transformation and loading
- **DAX** - Advanced calculations and measures

## 📁 Data Architecture

### Data Sources
Three core tables from SQL Server:

| Table | Description | Key Fields |
|-------|-------------|------------|
| `ALX_OFF_LOGS_HIST` | Log details with timestamps and delay reasons | EFJ_HEADER_ID, Creation_Date, REASONS_FOR_DELAY, STATUS_ID |
| `ALX_OFF_CARRIERS_HIST` | Carrier and vendor information | Carrier_Num, Vendor_Name |
| `ALX_OFF_LOAD_HISTORY_INFO_HIST` | Load, customer, and office data | Load_ID, Customer_Name, Office, Load_Manager |

### SQL Query

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
and Convert(Date,L.Creation_Date) > '2024-12-31'```

## ?? Dashboard Components

### KPI Cards
- Total Loads Processed
- Delayed Loads Count
- On-Time Performance %
- Average Delay Duration

### Visualizations
- **Time Series Analysis** - Load trends over time
- **Carrier Performance Matrix** - Comparative carrier analysis
- **Delay Reason Pareto** - Top delay causes
- **Geographic Distribution** - Office and location-based performance
- **Agent Performance** - Load manager effectiveness tracking

## ?? Key Insights Delivered

- ? **Operational Efficiency** - Identify bottlenecks and improvement areas
- ? **Carrier Management** - Data-driven carrier selection and evaluation
- ? **Delay Root Cause Analysis** - Understand and address delay patterns
- ? **Office Performance** - Compare performance across locations
- ? **Customer Service** - Track service levels by customer

## ?? Business Impact

- **Reduced Delays** - Proactive identification of delay causes
- **Improved Carrier Relations** - Objective performance metrics
- **Enhanced Decision Making** - Real-time visibility into operations
- **Cost Optimization** - Better resource allocation based on data
- **Customer Satisfaction** - Improved on-time delivery rates

## ?? Setup & Usage

### Prerequisites
- Power BI Desktop (latest version)
- SQL Server access with appropriate permissions
- Network connectivity to data source

### Installation
1. Clone this repository
2. Open the Power BI file
3. Update data source connections
4. Refresh data to load latest information

### Data Refresh
- Scheduled refresh configured for daily updates
- Manual refresh available via Power BI Desktop

## ?? Project Structure

```
PowerBI-Logistics-Performance-Dashboard/
�
+-- README.md                    # This file
+-- image (2).png               # Dashboard screenshot
+-- [Power BI File]             # Main dashboard file (if included)
```

## ?? Skills Demonstrated

- **Power BI Development** - Advanced dashboard design
- **SQL Querying** - Complex join operations and data extraction
- **DAX Programming** - Custom measures and calculations
- **Power Query M** - Data transformation and cleaning
- **Data Modeling** - Efficient relationship design
- **Business Intelligence** - Translating requirements to solutions

## ?? Future Enhancements

- [ ] Predictive analytics for delay forecasting
- [ ] Mobile-optimized view
- [ ] Automated alerting for critical delays
- [ ] Integration with carrier tracking systems
- [ ] Advanced ML-based anomaly detection

## ?? Contact

**Abhishek Zine**
- Email: abhishekzine201@gmail.com
- GitHub: [@Abhishek-zine](https://github.com/Abhishek-zine)

## ?? License

This project is available for portfolio and educational purposes.

---

**Built with Power BI** | **Last Updated: December 2025**
