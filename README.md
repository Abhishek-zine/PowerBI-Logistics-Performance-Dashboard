# 🚛 Power BI Logistics Performance Dashboard

**An interactive dashboard for carrier performance analysis, delay tracking, and load efficiency insights.**

---

## 📋 Project Summary

This Power BI dashboard addresses the challenge of monitoring and improving logistics performance across carrier operations. By consolidating data from multiple SQL Server tables, the dashboard provides real-time visibility into carrier reliability, delay patterns, and customer-level performance metrics. This enables operations teams to identify bottlenecks, reduce delays, and make data-driven decisions that improve overall logistics efficiency.

---

## 👤 Role: Power BI Developer

**Key Responsibilities:**
- **Data Modeling:** Designed star schema connecting log, carrier, and load history tables
- **DAX Development:** Created measures for on-time performance, delay analysis, and carrier ranking
- **Power Query (M):** Built data transformation and cleansing workflows
- **Visual Design:** Developed interactive visualizations with drill-through capabilities
- **Performance Tuning:** Optimized query folding and reduced report load times

---

## 🛠️ Technologies Used

| Technology | Purpose |
|------------|---------|
| Power BI Desktop | Dashboard development and visualization |
| DAX | Measures, calculated columns, and KPIs |
| SQL Server | Data source and query optimization |
| Power Query (M) | Data extraction, transformation, and loading |

---

## 📊 Data Sources

Three tables from SQL Server:

| Table | Description |
|--------|--------------|
| `ALX_OFF_LOGS_HIST` | Log details (creation date, delay reasons, status) |
| `ALX_OFF_CARRIERS_HIST` | Carrier/vendor data |
| `ALX_OFF_LOAD_HISTORY_INFO_HIST` | Load, customer, and office data |

**Data Refresh:** Manual refresh via Power BI Desktop (schedule refresh available when published to Power BI Service)

<details>
<summary>SQL Query Used</summary>

```sql
SELECT DISTINCT 
  L.EFJ_HEADER_ID,
  L.Log_ID,
  CONVERT(Date, L.Creation_Date) AS Creation_Date_Only,
  L.Creation_Date,
  L.REASONS_FOR_DELAY,
  L.STATUS_ID,
  L.Comments,
  LEFT(L.Comments, CHARINDEX(' ', L.Comments) - 1) AS Comments_Carrier_Number_Uncovered,
  C.Vendor_Name AS Vendor_Name_Uncovered,
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
FROM alctms.ALX_OFF_LOGS_HIST L
LEFT JOIN alctms.ALX_OFF_CARRIERS_HIST C 
  ON C.Carrier_Num = LEFT(L.Comments, CHARINDEX(' ', L.Comments) - 1)
LEFT JOIN alctms.ALX_OFF_LOAD_HISTORY_INFO_HIST I 
  ON L.EFJ_HEADER_ID = I.EFJ_HEADER_ID
WHERE L.STATUS_ID = '21'
  AND CONVERT(Date, L.Creation_Date) > '2024-12-31'
```

</details>

---

## 📈 Key Results & Metrics

| Metric | Value |
|--------|-------|
| Dashboard Load Time | _[Placeholder: Add measured time]_ |
| Data Model Size | _[Placeholder: Add PBIX file size]_ |
| Report Pages | _[Placeholder: Number of pages]_ |
| Key Insights Delivered | On-time performance trends, carrier reliability ranking, delay reason analysis |

---

## 🖼️ Screenshots

> Add screenshots to the `assets/screenshots/` folder and reference them below:

```markdown
![Dashboard Overview](assets/screenshots/dashboard-preview.png)
![Data Model](assets/screenshots/data-model.png)
```

**Current Dashboard Preview:**

![Dashboard Preview](image%20(2).png)

---

## 🚀 How to Run / View the Report

### Prerequisites
- [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free download)

### Steps
1. Clone this repository or download the PBIX file
2. Open the `.pbix` file with Power BI Desktop
3. If prompted, update data source credentials for SQL Server connection
4. Click "Refresh" to load the latest data (requires database access)
5. Navigate through report pages to explore insights

> **Note:** The dashboard requires access to the source SQL Server database for data refresh. Without database access, you can still view the report structure and sample data.

---

## 📁 Project Structure

```
├── README.md                    # Project documentation
├── portfolio-metadata.json      # Structured metadata for portfolio
├── assets/
│   └── screenshots/             # Dashboard screenshots
├── .github/
│   └── pull_request_template.md # PR template for contributions
└── *.pbix                       # Power BI report file (if included)
```

---

## 📄 License

_[Placeholder: Add license information (e.g., MIT, Apache 2.0, or proprietary)]_

---

## 🔗 Contact

For questions about this project or collaboration opportunities, please reach out via GitHub.
