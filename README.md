# Retail_Sales_Analytics.sql

CREATE DATABASE IF NOT EXISTS retail_db;
USE retail_db;
CREATE TABLE retail_sales (
    order_id INT,
    order_date DATE,
    product STRING,
    category STRING,
    region STRING,
    sales INT
);
INSERT INTO retail_sales VALUES
(101, '2024-01-01', 'Laptop', 'Electronics', 'South', 50000),
(102, '2024-01-02', 'Mobile', 'Electronics', 'North', 30000),
(103, '2024-01-03', 'Shoes', 'Fashion', 'East', 5000),
(104, '2024-01-04', 'TV', 'Electronics', 'West', 40000),
(105, '2024-01-05', 'Jeans', 'Fashion', 'South', 7000),
(106, '2024-01-06', 'Laptop', 'Electronics', 'North', 52000),
(107, '2024-01-07', 'Shoes', 'Fashion', 'West', 6000);

SELECT * FROM retail_sales;
#Total sales by region
SELECT
    region,
    SUM(sales) AS total_sales
FROM retail_sales
GROUP BY region;

#Top 3 selling products
SELECT
    product,
    SUM(sales) AS total_sales
FROM retail_sales
GROUP BY product
ORDER BY total_sales DESC
LIMIT 3;


#Top product per category

SELECT
    category,
    product,
    total_sales
FROM (
    SELECT
        category,
        product,
        SUM(sales) AS total_sales,
        ROW_NUMBER() OVER (PARTITION BY category ORDER BY SUM(sales) DESC) AS rn
    FROM retail_sales
    GROUP BY category, product
) t
WHERE rn = 1;

#Sales by date
SELECT
    order_date,
    SUM(sales) AS daily_sales
FROM retail_sales
GROUP BY order_date
ORDER BY order_date;



