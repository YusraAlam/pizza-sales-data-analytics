# 🍕 Pizza Sales Performance Dashboard | SQL & Power BI

An end-to-end **Pizza Sales Analytics project** built using **SQL and Microsoft Power BI** to analyze sales performance, customer ordering patterns, product performance, revenue trends, and pizza category/size preferences.

This project demonstrates how raw transactional sales data can be transformed into meaningful business insights using **SQL analysis, data modeling, DAX, and interactive Power BI visualizations**.

---

## 📊 Dashboard Preview

![Pizza Sales Performance Dashboard](./dashboard.png)

---

## 🚀 Project Overview

The objective of this project is to analyze pizza sales data and answer important business questions such as:

- What is the total revenue generated?
- How many orders were placed?
- How many pizzas were sold?
- What is the average order value?
- What is the average number of pizzas per order?
- Which pizzas generate the highest revenue?
- Which pizzas have the lowest sales performance?
- Which pizza categories contribute the most to revenue?
- Which pizza sizes are most popular?
- Which days and months generate the highest sales?
- Which pizzas receive the highest number of orders?

The analysis was performed using **SQL**, while **Power BI** was used to build an interactive dashboard for business reporting and visualization.

---

# 🔄 Project Workflow

The project follows a practical data analytics workflow:

Raw Pizza Sales Dataset ↓ Data Cleaning & Preparation ↓ SQL Data Analysis ↓ Business KPI Calculation ↓ Power BI Data Modeling ↓ DAX Measures ↓ Interactive Dashboard ↓ Business Insights


---

# 🛠️ Tools & Technologies

Tool / Technology	Purpose
🗄️ SQL	Data analysis and business queries
📊 Microsoft Power BI	Interactive dashboard and visualization
🔄 Power Query	Data transformation and preparation
📈 DAX	KPI calculations and analytical measures
📁 CSV / Dataset	Source transactional sales data
📌 Key Performance Indicators
The dashboard tracks the following major KPIs:

KPI	Value
💰 Total Revenue	$817.62K
🧾 Total Orders	21,334
🍕 Total Pizzas Sold	49,559
🛒 Average Order Value	$38.32
🍕 Average Pizzas Per Order	2.32
📊 Dashboard Features
1️⃣ Monthly Revenue Trend
The monthly revenue trend visualizes how revenue changes throughout the year.

It helps identify:

Highest revenue months
Lowest revenue months
Seasonal sales patterns
Monthly revenue fluctuations
Overall sales trends
2️⃣ Sales Distribution by Pizza Category
Revenue is analyzed across different pizza categories:

Classic
Supreme
Chicken
Veggie
This analysis helps identify which pizza categories contribute the most to overall revenue.

3️⃣ Sales Distribution by Pizza Size
Revenue is also analyzed based on pizza size:

Small
Medium
Large
X-Large
XX-Large
This helps understand customer preferences and the contribution of different pizza sizes to total sales.

4️⃣ Orders by Day of Week
The dashboard analyzes order volume across:

Sunday
Monday
Tuesday
Wednesday
Thursday
Friday
Saturday
This helps identify the busiest and slowest days of the week.

5️⃣ Total Pizzas Sold by Size & Category
This visual compares pizza quantity sold across:

Pizza Size
Pizza Category
It helps identify the most popular combinations of pizza size and category.

6️⃣ Pizza Performance Analysis
The dashboard identifies the best and worst-performing pizzas based on different business metrics.

🏆 Top Pizza by Revenue
The Thai Chicken Pizza

🏆 Top Pizza by Orders
The Classic Deluxe Pizza

🏆 Top Pizza by Quantity Sold
The Classic Deluxe Pizza

⚠️ Lowest Performing Pizza
The Brie Carre Pizza

These insights can help management improve menu strategy, promotions, and product positioning.

🗄️ SQL Analysis
SQL was used to perform the core business analysis on the pizza_sales dataset.

📌 Main Dataset Table
pizza_sales
Important Columns
order_id
order_date
pizza_name
pizza_category
pizza_size
quantity
total_price
📈 SQL Queries
1. Total Revenue
SELECT 
    SUM(total_price) AS Total_Revenue
FROM pizza_sales;
2. Average Order Value
SELECT 
    CAST(
        CAST(SUM(total_price) AS DECIMAL(10,2)) /
        CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2))
        AS DECIMAL(10,2)
    ) AS Avg_Order_Value
FROM pizza_sales;
3. Total Pizzas Sold
SELECT 
    SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales;
4. Total Orders
SELECT 
    COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales;
5. Average Pizzas Per Order
SELECT 
    CAST(
        CAST(SUM(quantity) AS DECIMAL(10,2)) /
        CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2))
        AS DECIMAL(10,2)
    ) AS Avg_Pizzas_Per_Order
FROM pizza_sales;
📊 Business Analysis Queries
6. Daily Trend for Total Orders
SELECT 
    TO_CHAR(order_date, 'DAY') AS order_day,
    COUNT(DISTINCT order_id) AS total_orders
FROM pizza_sales
GROUP BY TO_CHAR(order_date, 'DAY');
7. Monthly Trend for Orders
SELECT 
    TO_CHAR(order_date, 'MONTH') AS order_month,
    COUNT(DISTINCT order_id) AS total_orders
FROM pizza_sales
GROUP BY TO_CHAR(order_date, 'MONTH');
8. Percentage of Sales by Pizza Category
SELECT 
    pizza_category,
    CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_revenue,
    CAST(
        SUM(total_price) * 100 /
        (SELECT SUM(total_price) FROM pizza_sales)
        AS DECIMAL(10,2)
    ) AS PCT
FROM pizza_sales
GROUP BY pizza_category;
9. Percentage of Sales by Pizza Size
SELECT 
    pizza_size,
    CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_revenue,
    CAST(
        SUM(total_price) * 100 /
        (SELECT SUM(total_price) FROM pizza_sales)
        AS DECIMAL(10,2)
    ) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;
10. Total Pizzas Sold by Pizza Category
SELECT 
    pizza_category,
    SUM(quantity) AS Total_Quantity_Sold
FROM pizza_sales
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;
🏆 Top & Bottom Performing Pizzas
11. Top 5 Pizzas by Revenue
SELECT 
    pizza_name,
    SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC
LIMIT 5;
12. Bottom 5 Pizzas by Revenue
SELECT 
    pizza_name,
    SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC
LIMIT 5;
13. Top 5 Pizzas by Quantity
SELECT 
    pizza_name,
    SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
LIMIT 5;
14. Bottom 5 Pizzas by Quantity
SELECT 
    pizza_name,
    SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
LIMIT 5;
15. Top 5 Pizzas by Total Orders
SELECT 
    pizza_name,
    COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC
LIMIT 5;
16. Bottom 5 Pizzas by Total Orders
SELECT 
    pizza_name,
    COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC
LIMIT 5;
🔎 Filter-Based Analysis
The SQL queries can be modified using the WHERE clause to perform category- or size-specific analysis.

Example: Classic Pizza Category
SELECT 
    pizza_name,
    COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
WHERE pizza_category = 'Classic'
GROUP BY pizza_name
ORDER BY Total_Orders DESC
LIMIT 5;
Example: Chicken Pizza Category
SELECT 
    pizza_name,
    COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
WHERE pizza_category = 'Chicken'
GROUP BY pizza_name
ORDER BY Total_Orders DESC
LIMIT 5;
Example: Large Pizza Size
SELECT 
    pizza_name,
    SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
WHERE pizza_size = 'Large'
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
LIMIT 5;
These filters allow deeper product-level analysis.

💡 Key Business Insights
Based on the dashboard analysis, several important insights can be identified.

🍕 Product Performance
The Thai Chicken Pizza generates the highest revenue.
The Classic Deluxe Pizza performs strongly in terms of both orders and quantity sold.
The Brie Carre Pizza appears among the lowest-performing pizzas.
📅 Sales Trends
Revenue fluctuates throughout the year.
Order volume varies across different days of the week.
Thursday shows one of the highest order volumes in the weekly analysis.
📦 Pizza Size
Large pizzas contribute significantly to overall sales.
Medium and Large sizes represent important portions of the sales mix.
Smaller and extra-large sizes contribute comparatively less.
🏷️ Category Performance
Classic, Supreme, Chicken, and Veggie pizzas contribute differently to overall revenue.
Category-level analysis can help improve menu positioning and promotional strategies.
🎯 Business Recommendations
Based on the analysis, the following business strategies can be considered:

1. Promote High-Performing Products
Focus marketing campaigns and promotional offers on pizzas with high revenue and order volumes.

2. Analyze Low-Performing Products
Review pricing, ingredients, customer feedback, and menu positioning for consistently low-performing pizzas.

3. Optimize Promotions by Day
Use day-of-week sales patterns to introduce targeted promotions during slower sales periods.

4. Leverage Popular Pizza Sizes
Create combo deals and family offers around the most frequently purchased pizza sizes.

5. Improve Menu Strategy
Use revenue, quantity, and order-level metrics together to identify products that are both popular and commercially valuable.

6. Data-Driven Decision Making
Use the dashboard regularly to monitor changes in product performance, customer preferences, and revenue trends.

📁 Project Structure
The recommended GitHub repository structure is:

Pizza-Sales-Analysis/
│
├── 📊 Dashboard/
│   └── Pizza_Sales_Dashboard.pbix
│
├── 🗄️ SQL/
│   └── Pizza_Sales_SQL_Queries.sql
│
├── 📁 Dataset/
│   └── pizza_sales.csv
│
├── 🖼️ Images/
│   └── dashboard.png
│
└── README.md
📊 KPI Summary
KPI	Value
💰 Total Revenue	$817.62K
🧾 Total Orders	21,334
🍕 Total Pizzas Sold	49,559
🛒 Average Order Value	$38.32
🍕 Average Pizzas Per Order	2.32
🧠 Skills Demonstrated
This project demonstrates practical skills in:

SQL
Data Analysis
Data Aggregation
Business KPI Development
Microsoft Power BI
Power Query
DAX
Data Modeling
Data Visualization
Trend Analysis
Product Performance Analysis
Category & Size Analysis
Business Intelligence
Dashboard Development
Insight-Driven Storytelling
🎯 Project Objective
The primary objective of this project is to demonstrate how raw transactional sales data can be transformed into actionable business insights using SQL and Power BI.

The dashboard enables stakeholders to quickly understand:

What is selling, how much is being sold, when customers are ordering, and which products are driving revenue.
👩‍💻 Author
Yusra Alam
Aspiring Data Analyst passionate about transforming raw data into meaningful business insights using:

SQL • Power BI • Python • Excel • Data Analytics

⭐ If You Found This Project Useful
If you found this project helpful or interesting, consider giving the repository a ⭐ Star.

📌 Project Highlights
Domain: Food & Beverage Analytics Project Type: Business Intelligence / Data Analytics Primary Tools: SQL & Power BI Focus Areas: Sales Analysis, KPI Tracking, Product Performance, Revenue Trends, Business Insights

🍕 Thank You for Visiting!
