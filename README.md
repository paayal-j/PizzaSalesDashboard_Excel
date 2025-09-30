# PizzaSalesDashboard_Excel
PIZZA SALES SQL QUERIES
# A. KPI’s
1. Total Revenue:
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
 <img width="183" height="84" alt="image" src="https://github.com/user-attachments/assets/688332c1-ffd9-4ed9-ba3f-d6576d01a27f" />

2. Average Order Value
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales
 <img width="195" height="85" alt="image" src="https://github.com/user-attachments/assets/b41d8ea9-ce06-4439-8ed0-cde937b25c47" />

3. Total Pizzas Sold
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales
 <img width="199" height="86" alt="image" src="https://github.com/user-attachments/assets/39286d01-da37-49d7-93b1-bb0dffe7b319" />

4. Total Orders
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales
 <img width="202" height="82" alt="image" src="https://github.com/user-attachments/assets/9208b8fb-23a9-4055-93db-7d4411b4d976" />

5. Average Pizzas Per Order
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales
 <img width="208" height="90" alt="image" src="https://github.com/user-attachments/assets/17468fec-1f61-4786-bab6-68607cb1477b" />

# B. Daily Trend for Total Orders
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date)
Output:
 <img width="235" height="208" alt="image" src="https://github.com/user-attachments/assets/6730a3e0-144f-4e6d-8106-d182f022d007" />

# C. Hourly Trend for Orders
SELECT DATEPART(HOUR, order_time) as order_hours, COUNT(DISTINCT order_id) as total_orders
from pizza_sales
group by DATEPART(HOUR, order_time)
order by DATEPART(HOUR, order_time)
Output
 <img width="265" height="371" alt="image" src="https://github.com/user-attachments/assets/660def87-101d-4a4c-afad-cdf62006fbc9" />

# D. % of Sales by Pizza Category
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category
Output
 <img width="385" height="176" alt="image" src="https://github.com/user-attachments/assets/2dcd7020-9d43-48d4-b479-4b922db5b52b" />

# E. % of Sales by Pizza Size
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size
Output
 <img width="351" height="203" alt="image" src="https://github.com/user-attachments/assets/963d0bf0-9772-4ead-90bb-ce9d11fa22b2" />


# F. Total Pizzas Sold by Pizza Category
SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC
Output
 <img width="362" height="174" alt="image" src="https://github.com/user-attachments/assets/be78358b-5f54-4416-8700-c4157e185885" />

# G. Top 5 Best Sellers by Total Pizzas Sold
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
Output
 <img width="458" height="181" alt="image" src="https://github.com/user-attachments/assets/7bf3b84f-b1ea-4ab6-96bb-8980de431c75" />





# H. Bottom 5 Best Sellers by Total Pizzas Sold
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
Output
 <img width="427" height="195" alt="image" src="https://github.com/user-attachments/assets/03b3500a-3198-4fb2-9c7e-baed41d0c1fd" />


# NOTE
If you want to apply the Month, Quarter, Week filters to the above queries you can use WHERE clause. Follow some of below examples
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
WHERE MONTH(order_date) = 1
GROUP BY DATENAME(DW, order_date)

*Here MONTH(order_date) = 1 indicates that the output is for the month of January. MONTH(order_date) = 4 indicates output for Month of April.

SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
WHERE DATEPART(QUARTER, order_date) = 1
GROUP BY DATENAME(DW, order_date)

*Here DATEPART(QUARTER, order_date) = 1 indicates that the output is for the Quarter 1. MONTH(order_date) = 3 indicates output for Quarter 3.
