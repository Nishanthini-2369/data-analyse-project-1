# Pizza Sales Dashboard Project (SQL + Excel)
## Project Objective
The goal of this project is to study pizza sales data using SQL and Excel. It helps to:
  1)Find out when people buy the  pizzas
  2)See which pizza sizes and categories are most popular
  3)Identify the best and worst-selling pizzas
  4)Give useful ideas to help improve sales and customer experience
## Data Set Used
-<a href="https://github.com/Nishanthini-2369/data-analyse-project-1/blob/main/pizza%20sales%20analysis.xlsx">Dataset</a>
## Qustions KPI's
-What is the daily trend of total pizza orders?
-What is the hourly trend of orders during the day?
-What percentage of sales comes from each pizza category?
-What percentage of sales comes from each pizza size?
-How many pizzas are sold in each category?
-Which are the top 5 best-selling pizzas?
-Which are the bottom 5 worst-selling pizzas?

## Dashboard Interaction 
-<a href="https://github.com/Nishanthini-2369/data-analyse-project-1/blob/main/Screenshot%202025-05-18%20132729.png">View Dashboard</a>
## Process
Import Data – Loaded the pizza sales dataset into SQL Server.
Clean Data – Fixed missing values and corrected data types.
Write Queries – Created SQL queries to answer business questions.
Analyze Results – Studied the query results to find patterns and insights.
Visualize Data – Used Excel (or Power BI) to make charts and dashboards.

## Dashboards![Screenshot 2025-05-18 132729](https://github.com/user-attachments/assets/bc1a9a37-f039-4a03-aab0-b655a19d5909)

## Sql Queries
--A KPI’s
--1 Total Revenue:
SELECT SUM(total_price) AS Total_Revenue FROM [pizza_sales (3)]

--2 Average Order Value
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM [pizza_sales (3)]

--3 Total Pizzas Sold
SELECT SUM(quantity) AS Total_pizza_sold FROM [pizza_sales (3)]

--4 Total Orders
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM [pizza_sales (3)]

--5 Average Pizzas Per Order
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM [pizza_sales (3)]

--B Daily Trend for Total Orders
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM [pizza_sales (3)]
GROUP BY DATENAME(DW, order_date)

--C Hourly Trend for Orders
SELECT DATEPART(HOUR, order_time) as order_hours, COUNT(DISTINCT order_id) as total_orders
from [pizza_sales (3)]
group by DATEPART(HOUR, order_time)
order by DATEPART(HOUR, order_time)

--D % of Sales by Pizza Category
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from [pizza_sales (3)]) AS DECIMAL(10,2)) AS PCT
FROM [pizza_sales (3)]
GROUP BY pizza_category

--E % of Sales by Pizza Size
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from [pizza_sales (3)]) AS DECIMAL(10,2)) AS PCT
FROM [pizza_sales (3)]
GROUP BY pizza_size
ORDER BY pizza_size

--F Total Pizzas Sold by Pizza Category
SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM [pizza_sales (3)]
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC

--G Total Pizzas Sold by Pizza Size
SELECT pizza_size, SUM(quantity) as Total_Quantity_Sold
FROM [pizza_sales (3)]
WHERE MONTH(order_date) = 2
GROUP BY pizza_size
ORDER BY Total_Quantity_Sold DESC


--H Bottom 5 Best Sellers by Total Pizzas Sold
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM [pizza_sales (3)]
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
## SQl Queries link
-<a href="https://github.com/Nishanthini-2369/data-analyse-project-1/blob/main/pizza%20sales%20Sql%20quries.sql">View Sql Queries</a>

## Project Insights
-Total Revenue and Order Volume indicate stable business performance.
-Friday and Saturday have the highest number of orders, showing weekend preference.
-Large-sized and Classic category pizzas contribute the most to total revenue.
-The bottom 5 selling pizzas have low demand and may need promotion or replacement.

## project conclusiion
The pizza sales analysis reveals strong weekend and mealtime demand.
Large and classic pizzas are the top revenue contributors.
Sales trends help identify customer preferences and peak hours.
Insights can guide menu, marketing, and inventory strategies.

