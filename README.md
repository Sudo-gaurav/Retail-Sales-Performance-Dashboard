# Retail Sales Performance Dashboard

An interactive Power BI dashboard that analyzes retail sales performance across products, stores, and regions. This project demonstrates the integration of large datasets using SQL for data joining, Python for initial data inspection, and Power BI for dashboard creation.

---

## Table of Contents

- [Overview](#overview)
- [Repository Structure](#repository-structure)
- [Tools & Technologies](#tools--technologies)
- [Data Processing Workflow](#data-processing-workflow)
- [Code Snippets](#code-snippets)
- [Dashboard Highlights](#dashboard-highlights)
- [How to Run / Explore](#how-to-run--explore)
- [Additional Notes](#additional-notes)
- [License](#license)
- [Author](#author)

---

## Overview

Due to the large original retail sales dataset (>2GB), a cleaned sample dataset (<100MB) is provided. The full dataset is hosted externally (link available in `DATA/Full Retail Sales Dataset google drive link.txt`). This dashboard highlights key performance indicators like Total Sales, Total Revenue, Total Profit, and Profit Margin, with further insights through trends and comparisons by store type, product cluster, and city.

---

## Repository Structure
 retail-sales-performance-dashboard/ │ 
├── data/ │ ├── retail_sales_sample.csv  Sample cleaned dataset (<100 MB) │ 
  └── Full Retail Sales Dataset google drive link.txt # Link to the full 2+GB dataset hosted 
      externally
├── Retail_Sales_Performance_Dashboard.pbit # Power BI template dashboard file │ 
├── Retail_Sales_Dashboard.pdf # PDF snapshot of the dashboard │
├── README.md # Project documentation

---

## Tools & Technologies

- **SQL (PostgreSQL/pgAdmin 4):** Data loading, joining, and filtering.
- **Python (pandas):** Used for inspecting the column names of the large dataset.
- **Power BI (Power Query & Desktop):** Data transformation and interactive dashboard creation.
- **GitHub:** Version control and project sharing.

---

## Data Processing Workflow

1. **Data Preparation:**
   - Loaded the large retail sales dataset (>2GB) into PostgreSQL.
   - Joined it with supporting dimension tables (`store_cities` and `product_hierarchy`).
   - Filtered and cleaned the data, exporting a representative sample dataset.

2. **Inspection:**
   - A Python script was used to quickly inspect column names:
     ```python
     import pandas as pd

     # Load only headers from the large CSV
     df = pd.read_csv("Retail_Sales_Large.csv", nrows=0)
     print(df.columns.tolist())
     ```

3. **Dashboard Creation:**
   - The cleaned sample dataset was imported into Power BI via Power Query.
   - An interactive dashboard was built using KPI cards, line charts, and bar charts to show trends and comparisons across different dimensions.

---

## Code Snippets

### Python for Column Inspection

```python
import pandas as pd

# Load only headers from the large CSV
df = pd.read_csv("Retail_Sales_Large.csv", nrows=0)
print(df.columns.tolist())


### SQL for  Data Joining and Cleaning

```sql
CREATE OR REPLACE VIEW v_full_retail AS
SELECT 
    rs.order_id,
    rs.date,
    rs.sales,
    rs.revenue,
    rs.profit,
    rs.price,
    rs.product_id,
    ph.cluster_id,
    ph.hierarchy1_id,
    rs.store_id,
    sc.storetype_id,
    sc.city_id
FROM retail_sales rs
LEFT JOIN store_cities sc
    ON rs.store_id = sc.store_id
LEFT JOIN product_hierarchy ph
    ON rs.product_id = ph.product_id;

---
### dashboard highlights

- KPI Cards: Display Total Sales, Total Revenue, Total Profit, and Profit Margin.
- Monthly Trends: Line chart showing revenue trends over time.
- Store Analysis: Bar chart comparing sales across various store types.
- Geographical & Product Insights: Visuals detailing performance by city and product cluster.
- Interactive Slicers: For dynamic filtering by date, store type, cluster, and other dimensions.

## How to Run / Explore
Dashboard:

Open the Power BI template file (dashboards/Retail_Sales_Performance_Dashboard.pbit) using Power BI Desktop.

Interact with the dashboard using the built-in slicers (e.g., date range, store type, cluster).

Dataset:

The file data/retail_sales_sample.csv is the cleaned sample used in the dashboard.
For the full dataset (2+GB), please refer to the download link provided in data/full_retail_sales_data_link.txt.
Static Report:
View reports/Retail_Sales_Dashboard.pdf for a snapshot view of the dashboard.

---

### Additional Notes
File Size Consideration:
Due to GitHub's file size limitations, only a sample dataset is included. The full dataset (~2+GB) is available via an external link in data/full_retail_sales_dataset_link.txt.

Future Enhancements:
Future updates may include enhanced drill-down features, dynamic tooltips, and additional visual insights based on further analysis.

---

### License
This project is licensed under the MIT License.

### Author
Gaurav Tawri
Gauravtawri007@gmail.com

