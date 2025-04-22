# 🍕 Pizza Sales Dashboard
This project is a Pizza Sales Dashboard built to visualize and analyze sales performance for a pizza restaurant. The dashboard provides valuable insights into sales trends, order patterns, customer preferences, and best-selling products.

![image alt](https://github.com/Sanchit2104/Pizza-Sales-Dashboard/blob/main/Screenshot%20(28).png?raw=true)

# 📊 Project Overview
The dashboard is designed to help stakeholders make data-driven decisions by providing:

Monthly and hourly sales trends

Sales breakdown by pizza category and size

Best and worst-selling pizzas

Average order value and pizzas per order

Peak order times and busiest months

# 🧩 Key Insights
Total Revenue: $817,860

Average Order Value: $38.30

Total Orders: 21,350

Total Pizzas Sold: 49,574

Avg Pizzas per Order: 2.32

# 🗓️ Busiest Days and Times
Orders are highest in July and August

Peak hours are 12:00 PM – 1:00 PM and 4:00 PM – 8:00 PM

# 🍕 Sales by Category & Size
Classic and Chicken categories drive the most sales

Large size pizzas contribute the most to sales volume

# 📈 Top 5 Best-Selling Pizzas
The Classic Deluxe Pizza

The Barbecue Chicken Pizza

The Hawaiian Pizza

The Pepperoni Pizza

The Thai Chicken Pizza

# 📉 Bottom 5 Worst-Selling Pizzas
Brie Carre Pizza (lowest seller)

The Soppressata Pizza

The Spinach Supreme Pizza

The Calabrese Pizza

The Greek Pizza

# 💾 SQL Queries Used
# A. KPI Queries
-- Total Revenue
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;

-- Average Order Value
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales;

-- Total Pizzas Sold
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;

-- Total Orders
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;

-- Average Pizzas Per Order
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2)) 
AS Avg_Pizzas_per_order FROM pizza_sales;
# B. Daily and Hourly Trends
-- Daily Trend for Total Orders
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales GROUP BY DATENAME(DW, order_date);

-- Hourly Trend for Orders
SELECT DATEPART(HOUR, order_time) AS order_hours, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales GROUP BY DATEPART(HOUR, order_time) ORDER BY DATEPART(HOUR, order_time);
# C. Sales by Category and Size
-- % of Sales by Pizza Category
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales GROUP BY pizza_category;

-- % of Sales by Pizza Size
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales GROUP BY pizza_size ORDER BY pizza_size;
# D. Top and Bottom Sellers
-- Top 5 Best Sellers
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold 
FROM pizza_sales GROUP BY pizza_name ORDER BY Total_Pizza_Sold DESC;

-- Bottom 5 Worst Sellers
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold 
FROM pizza_sales GROUP BY pizza_name ORDER BY Total_Pizza_Sold ASC;
# E. Monthly & Quarterly Filters (Example)
-- January Orders
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales WHERE MONTH(order_date) = 1 GROUP BY DATENAME(DW, order_date);

-- Quarter 1 Orders
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales WHERE DATEPART(QUARTER, order_date) = 1 GROUP BY DATENAME(DW, order_date);
# 🛠️ Tools & Technologies Used
Excel for data visualization

SQL Server / MySQL for querying the data

Spreadsheet / CSV for data storage (assumed)

🎯 Purpose
This project aims to:

Practice data storytelling and dashboard design using Advanced Excel Techniques

Extract actionable insights from raw sales data

Demonstrate SQL skills for real-world analytics tasks
