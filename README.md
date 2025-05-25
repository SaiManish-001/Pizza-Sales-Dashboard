# Pizza-Sales-Dashboard

## Problem Statement

To evaluate the performance of our pizza business and uncover actionable insights, we aim to analyze key performance indicators (KPIs) derived from our sales data. The primary metrics to be calculated include:
1.	Total Revenue – The overall income generated from all pizza orders by summing up their total prices.
2.	Average Order Value – The mean spend per order, calculated by dividing the total revenue by the number of orders placed.
3.	Total Pizzas Sold – The cumulative quantity of pizzas sold across all transactions.
4.	Total Orders – The total count of unique orders processed.
5.	Average Pizzas per Order – The mean number of pizzas per order, calculated by dividing the total pizzas sold by the total orders.

## Visualization Requirements – Charts & Dashboards

To gain a deeper understanding of trends and customer behavior, we plan to use various visualizations. The following charts are required to represent our sales data:
1.	Hourly Sales Trend (Total Pizzas Sold)
o	Develop a stacked bar chart showing pizza sales per hour over a selected timeframe. This will help reveal peak sales hours and hourly ordering patterns.
2.	Weekly Sales Trend (Total Orders)
o	Build a line chart to depict how total order volumes vary each week throughout the year, helping identify seasonal spikes or dips.
3.	Sales Distribution by Pizza Category
o	Create a pie chart showing the proportion of sales across different pizza categories. This will offer insights into customer preferences by category.
4.	Sales Distribution by Pizza Size
o	Present a pie chart illustrating the percentage contribution of each pizza size to total sales. This will help assess the popularity of different pizza sizes.
5.	Total Pizzas Sold by Category
o	Design a funnel chart displaying the number of pizzas sold by category to easily compare performance between categories.
6.	Top 5 Best-Selling Pizzas
o	Generate a bar chart highlighting the top 5 pizzas based on three key metrics: revenue, total quantity sold, and number of orders. This will help spotlight the most popular menu items.
7.	Bottom 5 Worst-Selling Pizzas
o	Create a bar chart for the bottom 5 pizzas in terms of revenue, quantity, and orders. This will help identify low-performing products that may need re-evaluation.

## Data Analysis using MySQL

### Data Import

![image](https://github.com/user-attachments/assets/211088c2-3457-4a66-a5cc-ba1d42fd4d3a)
![image](https://github.com/user-attachments/assets/c63d9f40-3ada-42fb-9bc4-4d595f2520af)


### KPIs

#### Total Revenue

`SELECT SUM(total_price) AS total_revenue FROM pizza_sales;`

![image](https://github.com/user-attachments/assets/6c550f4b-5e5c-4e26-9b6f-694386a7cc2f)

#### Average Order Value

`SELECT SUM(total_price) / COUNT(DISTINCT order_id) AS avg_order_value FROM pizza_sales;`

![image](https://github.com/user-attachments/assets/b9c317b0-2d56-43bd-bca9-5ef388917b39)

#### Total Pizzas Sold
`SELECT SUM(quantity) AS total_pizza_sold FROM pizza_sales;`

![image](https://github.com/user-attachments/assets/10fd0d0c-f9b6-4c26-8641-3105620e35b9)

#### Total Orders
`SELECT COUNT(DISTINCT order_id) AS total_order FROM pizza_sales;`

![image](https://github.com/user-attachments/assets/d8390591-cdec-46e3-80e9-f1dc967dcf58)

#### Average Pizzas per Order
`SELECT ROUND(SUM(quantity) / COUNT(DISTINCT order_id), 2) AS avg_pizza_per_order FROM pizza_sales;`

![image](https://github.com/user-attachments/assets/387e9ef7-bee2-44eb-8c9f-75297e9646b5)

### Hourly Trend for Total Pizzas Sold
`SELECT HOUR(order_time) AS order_hours, SUM(quantity) AS total_pizzas_sold
FROM pizza_sales
GROUP BY HOUR(order_time)
ORDER BY HOUR(order_time);`

![image](https://github.com/user-attachments/assets/1633e4a2-ffd2-4ece-9374-8f60f1d6ab55)

### Weekly Trend for Orders
`SELECT WEEK(order_date, 3) AS WeekNumber, YEAR(order_date) AS Year,
      COUNT(DISTINCT order_id) AS Total_orders
FROM pizza_sales
GROUP BY WEEK(order_date, 3), YEAR(order_date)
ORDER BY Year, WeekNumber;`

![image](https://github.com/user-attachments/assets/f1935bc3-8dd3-47f8-83fb-ff428e9101e9)

### % of Sales by Pizza Category
`SELECT pizza_category,
    ROUND(SUM(total_price), 2) AS total_revenue,
    ROUND(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales), 2) AS PCT
FROM pizza_sales 
GROUP BY pizza_category;`

![image](https://github.com/user-attachments/assets/792ab795-e5fd-404b-83cd-82acd058a330)

### % of Sales by Pizza Size
`SELECT pizza_size,
    ROUND(SUM(total_price), 2) AS total_revenue,
    ROUND(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales), 2) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;`

![image](https://github.com/user-attachments/assets/b87ed45b-cf11-41d1-b89d-3e7807d029aa)

### Total Pizzas Sold by Pizza Category
`SELECT pizza_category, SUM(quantity) AS Total_Quantity_Sold
FROM pizza_sales
-- WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;`

![image](https://github.com/user-attachments/assets/124db14b-e02b-41ef-9675-9637178f5d9e)

### Top 5 Pizzas by Revenue
`SELECT pizza_name, SUM(total_price) AS Total_Revenue
FROM  pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC LIMIT 5;`

![image](https://github.com/user-attachments/assets/2fcdbd68-f468-4e84-9a59-65a4ccca18fd)

### Bottom 5 Pizzas by Revenue
`SELECT pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC LIMIT 5;`

![image](https://github.com/user-attachments/assets/2ba8ae41-24df-4ed2-bd22-2fdfa132d063)

### Top 5 Pizzas by Quantity
`SELECT pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
 LIMIT 5;`
 
 ![image](https://github.com/user-attachments/assets/f2f4c764-91e4-42f2-a2cb-b6dfa8225e8a)

 ### Top 5 Pizzas by Total Orders
 `SELECT pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC
LIMIT 5;`

![image](https://github.com/user-attachments/assets/7dd6716f-3dd8-4c45-8ab8-28bc1c6d7b79)

### Bottom 5 Pizzas by Total Orders
`SELECT 
    pizza_name, 
    COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC
LIMIT 5;`

![image](https://github.com/user-attachments/assets/1ea255a9-5c05-45b5-b4c7-41fec83c1f13)


## Data Cleaning

![image](https://github.com/user-attachments/assets/8e2ea105-da45-420e-b228-3e3d4a9a1f9e)

## Building Dashboard Using Tableau

Developed a detailed Tableau dashboard showcasing essential KPIs and visual insights such as hourly sales patterns, weekly order trends, category-wise and size-wise sales distributions, total pizzas sold by category, as well as top and bottom 5 performing pizzas based on sales metrics.

### KPIs

- Total Revenue SUM([order id])
- Total Orders COUNTD([order id])
- Average Order Value [total revenue] / [total orders]
- Total Pizzas Sold SUM([quantity])
- Average Pizzas Per Order [total pizzas sold] / [total orders]

![image](https://github.com/user-attachments/assets/08dfa260-2901-4286-8008-a3afcdf836a2)

### Insights

![image](https://github.com/user-attachments/assets/a630eb49-bd82-47d1-9e39-ce56bb010c0f)


### Dashboards

![image](https://github.com/user-attachments/assets/ced78f4d-f0c1-42ac-b3e8-dc4521d9b0f4)

![image](https://github.com/user-attachments/assets/5fd43415-9176-40ef-aa91-e0d2414d472d)

## Tools Used

- MySQL
- Tableau
- Microsoft Excel
























