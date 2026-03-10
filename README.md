📊 Olist E‑commerce Data Analysis (SQL + Power BI)
This project is an analytical exploration of the Olist Brazilian E‑commerce dataset, performed using SQL and Power BI.
The goal is to understand sales performance, customer behavior, and product profitability.

🔧 Tools & Technologies
SQL (PostgreSQL / MySQL)
Power BI
Business Analysis

🧩 Project Tasks
✔️ SQL Analysis
Top product categories by total sales
Top products by sales volume
Top sellers by revenue
Unique customer distribution by city
Margin calculation: price – freight_value
Multi‑table JOINs (4+ tables)
Aggregations, grouping, sorting, filtering

✔️ Power BI Dashboard
Category‑level sales visualization
Revenue distribution by product category
Top cities by unique customers
Top products by revenue
Margin comparison across products

📈 Key Insights
health_beauty is the leading category by revenue.
garden_tools has the highest number of sold items.
São Paulo is the largest market by unique customers.
Several categories have multiple products in the top‑5 — strong demand concentration.
Freight cost significantly impacts product margin.

1. Number of orders by day
•	select date(order_purchase_timestamp) as order_day, 
•	count(*) as total_orders
•	from olist.orders
•	group by order_day
•	order by order_day asc;

2. Top 5 product categories by revenue
•	select pcnt.product_category_name_english as category_name,
•	sum(oi.price) as revenue
•	from orders o 
•	join order_items oi on oi.order_id = o.order_id
•	join products p on p.product_id = oi.product_id
•	join product_category_name_translation pcnt on pcnt.product_category_name = p.product_category_name
•	group by category_name
•	order by revenue DESC
•	limit 5;

3. Top 5 cities by number of unique customers
•	SELECT count(distinct c.customer_unique_id) as unique_people,
•	customer_city as city
•	FROM orders o
•	join customers c on c.customer_id = o.customer_id
•	group by city
•	order by unique_people desc
•	limit 5;

4. Top 5 sellers by total revenue
•	SELECT distinct seller_id as seller,
•	sum(price) revenue
•	FROM order_items
•	group by seller
•	order by revenue desc
•	limit 5;

5. Top 5 products by number of sales
•	SELECT 
•	oi.product_id,
•	pcnt.product_category_name_english AS category_name,
•	COUNT(*) AS total_sales
•	FROM order_items oi
•	JOIN products p ON p.product_id = oi.product_id
•	JOIN product_category_name_translation pcnt 
•	ON pcnt.product_category_name = p.product_category_name
•	GROUP BY oi.product_id, category_name
•	ORDER BY total_sales DESC
•	LIMIT 5;

6. Top 5 products by profit (price – freight_value)
•	SELECT pcnt.product_category_name_english products_name,
•	sum(price - freight_value) price,
•	p.product_id
•	FROM order_items oi
•	join products p on p.product_id = oi.product_id
•	join product_category_name_translation pcnt on pcnt.product_category_name = p.product_category_name
•	group by products_name, p.product_id
•	order by price desc
•	limit 5;

