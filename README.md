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

![image](https://github.com/user-attachments/assets/b9c317b0-2d56-43bd-bca9-5ef388917b39)

#### Total Pizzas Sold

![image](https://github.com/user-attachments/assets/10fd0d0c-f9b6-4c26-8641-3105620e35b9)

#### Total Orders

![image](https://github.com/user-attachments/assets/d8390591-cdec-46e3-80e9-f1dc967dcf58)

#### Average Pizzas per Order

![image](https://github.com/user-attachments/assets/387e9ef7-bee2-44eb-8c9f-75297e9646b5)








