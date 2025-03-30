# Retail Sales Dashboard – Power BI Project

## 🔍 Objective
Build a dynamic Power BI dashboard to help a fictional electronics retail company monitor sales performance, inventory status, and regional trends.

## 📊 Tools Used
- Power BI Desktop
- Power Query
- DAX for custom measures
- CSV file as data source

## 📁 Dataset Overview
Simulated daily sales data across 4 regions and multiple product categories:
- `retail_sales_data.csv`

**Fields include:**
- Date
- Region
- Product Category / Name
- Units Sold
- Revenue & Cost
- Inventory Remaining
- Return Flag

## 📈 Dashboard Features
- KPI Cards: Total Revenue, Units Sold, Average Order Value
- Line Chart: Monthly revenue trends
- Bar Charts: Product Category & Region comparisons
- Table: Low inventory alerts with conditional formatting
- Slicers: Region, Product Category, and Date

## ➕ Custom DAX Measures
```DAX
Average Order Value = 
DIVIDE(SUM('Raw Data'[Revenue]), SUM('Raw Data'[Units Sold]), 0)

Return Rate (%) = 
DIVIDE(
    CALCULATE(COUNTROWS('Raw Data'), FILTER('Raw Data', 'Raw Data'[Return] = "Yes")),
    COUNTROWS('Raw Data'),
    0
) * 100

Gross Margin (%) = 
DIVIDE(SUM('Raw Data'[Revenue]) - SUM('Raw Data'[Cost]), SUM('Raw Data'[Revenue]), 0) * 100

Inventory Turnover = 
DIVIDE(SUM('Raw Data'[Units Sold]), AVERAGE('Raw Data'[Inventory Remaining]), 0)
```

## 📅 Time Intelligence Support
Create a Date Table in Power BI for monthly trends:
```DAX
DateTable = 
ADDCOLUMNS(
    CALENDAR(DATE(2023,1,1), DATE(2023,12,31)),
    "Year", YEAR([Date]),
    "Month", FORMAT([Date], "MMMM"),
    "MonthNumber", MONTH([Date]),
    "YearMonth", FORMAT([Date], "YYYY-MM")
)
```
Then relate `Raw Data[Date]` to `DateTable[Date]`.

Optional Time Intelligence Measures:
```DAX
YTD Revenue = 
TOTALYTD(SUM('Raw Data'[Revenue]), 'DateTable'[Date])

MTD Units Sold = 
TOTALMTD(SUM('Raw Data'[Units Sold]), 'DateTable'[Date])
```

## 📂 Project Structure
```bash
/Retail_Sales_Dashboard/
├── retail_sales_data.csv
├── Retail_Sales_Dashboard.pbix
├── README.md
├── .gitignore
```

## 🔗 Connect
Let’s connect on [LinkedIn](https://www.linkedin.com/in/the-madonald) or [GitHub](https://github.com/themacdonald)

---

> "Good business decisions start with good data."
