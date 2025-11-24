# Retail-Sales-Analytics-End-to-End-SQL-Power-BI-Project
This project demonstrates a full end-to-end Business Intelligence workflow using a synthetic retail sales dataset. I built a normalized SQL database, created a star schema in Power BI, developed DAX measures, and delivered a multi-page dashboard presenting product insights, customer behavior, and executive-level KPIs.

The project showcases my ability to work across the entire analytics pipeline — from data engineering to visual analytics to executive storytelling.

Tools & Technologies
MySQL Workbench – Database design, SQL development
SQL – Joins, constraints, DDL, DML, data validation
Power BI Desktop – Data modeling, relationships, visuals
DAX – KPI measures and calculated logic
Excel – Supplementary data enrichment
GitHub – Version control and portfolio hosting

Skills Demonstrated
✔ SQL Development
✔ Database Schema Design (3NF)
✔ Star Schema Modeling
✔ Power BI Data Modeling
✔ DAX Calculations
✔ KPI Development
✔ Data Visualization Best Practices
✔ Analytical Storytelling
✔ Business Insight Generation
✔ End-to-End BI Solution Architecture

Database Architecture
The SQL database consists of four normalized tables:
Customers
Orders
OrderItems
Products
I created and enforced primary keys, foreign keys, and referential integrity.
The enriched product cost table was added to enable profit calculations.

Representative SQL Code (Schema Example)
CREATE TABLE Products (
    ProductID INT PRIMARY KEY AUTO_INCREMENT,
    ProductName VARCHAR(255),
    Category VARCHAR(100),
    UnitPrice DECIMAL(10,2),
    Cost DECIMAL(10,2)
);
SQL Joins for Validation
SELECT 
    c.FullName,
    o.OrderID,
    SUM(oi.Quantity * oi.UnitPrice) AS OrderAmount
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID
JOIN OrderItems oi ON o.OrderID = oi.OrderID
GROUP BY c.FullName, o.OrderID;

Power BI Data Model
I implemented a star schema:
Fact Table: OrderItems
Dimension Tables: Customers, Products, Orders
Correct cardinalities (1:* and *:1) and cross-filter behavior were configured to support DAX calculations.

DAX Measures (Examples)
Total Revenue = SUMX(OrderItems, OrderItems[Quantity] * OrderItems[UnitPrice])

Completed Revenue = CALCULATE([Total Revenue], Orders[Status] = "Completed")

Average Order Value = DIVIDE([Total Revenue], DISTINCTCOUNT(Orders[OrderID]))

AOV Completed = 
    DIVIDE(
        [Completed Revenue],
        CALCULATE(DISTINCTCOUNT(Orders[OrderID]), Orders[Status] = "Completed")
    )

Total Profit = 
SUMX(OrderItems, (OrderItems[Quantity] * OrderItems[UnitPrice]) - 
                 (OrderItems[Quantity] * OrderItems[Cost]))

Dashboard Pages
1. Executive Summary
Total Revenue: $3218
Completed Revenue: $2709
AOV (All Orders): $215
AOV Completed: $301
Order Count: 15 (9 completed)
Executive Insights
Completed orders drive 84% of revenue, showing strong fulfillment performance.
Higher AOV for completed orders indicates significant revenue upside from improved order completion.
Revenue is driven by higher-value purchases, especially premium furniture.
Opportunities exist to reduce order fallout and lift conversion rates.

2. Product Analysis
Visuals:
Quantity Sold by Product
Revenue by Product
Profit by Product
Product Insights (Concise)
Wireless Mouse sells the most units but produces the lowest revenue and profit, confirming it is a low-margin product.
Standing Desk generates the highest revenue and profit, making it the core profit driver.
Furniture outperforms accessories in profitability.
Mid-tier products (Keyboard & Headphones) show stable, balanced performance.

3. Customer Analysis
Visuals:
Revenue by Customer
Total Orders by Customer
Revenue Contribution (%)
Customer Insights
High-value customers contribute a disproportionate share of revenue.
Frequent purchasers tend to be the highest spenders.
Wide variance in spending suggests opportunities for targeted engagement and retention efforts.

End-to-End Workflow Summary
Designed a normalized SQL database
Loaded and validated data with SQL
Exported and connected database to Power BI
Created star schema with correct relationships
Developed DAX measures for revenue, profit, and KPIs
Built executive summary and analysis dashboards
Delivered actionable business insights

Business Impact
This dashboard enables leaders to:
Identify top-performing products
Understand customer value distribution
Improve revenue forecasting
Prioritize high-margin items
Reduce order fallout
Enhance customer engagement

Project Files
SQL schema (.sql dump)
Power BI PBIX file
Product enrichment Excel file
README (this file)
Dashboard screenshots
