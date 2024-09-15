# Retail-Sales-Analysis-dashboard-Power-Bi-Report-
This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA).This project is ideal for those who are starting their journey in data analysis.
 

Retail Sales Analysis SQL Project
 
	Submitted by:
•	Ibrar Ali					54199
Project Structure 
 Database Setup
•	Database Creation: The project starts by creating a database named  retail_sales_dw.
•	Table Creation: A table named  sales_data, products_data, customer_data, store_data, sales_cleaned_data is created to store the sales data. 
SQL QUIRES :
create database retail_sales_dw;
use retail_sales_dw

--This table will store transactional data from retail sales--
create table sales_data(
t_transaction_id int primary key,
p_product_id int,
c_customer_id int,
s_store_id int,
q_quantity int,
r_revenue decimal(10,1),
t_transaction_date date 
);

--This table stores product details--
create table products_data(
p_product_id int primary key,
p_product_name varchar(50) not null,
c_category varchar(25) not null,
p_price decimal(10,1)
);

--This table stores customer information--
create table customer_data(
c_customer_id int primary key,
c_customer_name varchar(50) not null,
g_gender varchar(15),
a_age int,
e_email varchar(25) not null
);

--This table contain store information--
create table store_data(
s_store_id int primary key,
s_store_location varchar(25) not null,
m_manager_name varchar(50) not null
);
--Load Data--
--Create final cleaned sales Table--
CREATE TABLE sales_cleaned_data (
t_transaction_id int primary key,
p_product_id int,
c_customer_id int,
s_store_id int,
q_quantity int,
r_revenue decimal(10, 1),
t_transaction_date date
);

Data Exploration & Cleaning
•	Record Count: Determine the total number of records in the dataset.
•	Customer Count: Find out how many unique customers are in the dataset.
•	Category Count: Identify all unique product categories in the dataset.
•	Null Value Check: Check for any null values in the dataset and delete records with missing data.


select sum(r_revenue) as total_revenue
from sales_cleaned_data;


select sum(q_quantity) as total_quantity_sold
from sales_cleaned_data;


select sum(q_quantity) as average_revenue_per_transaction
from sales_cleaned_data;

--removes duplicate records--
select t_transaction_id, COUNT(*) 
FROM sales_data
GROUP BY t_transaction_id 
HAVING COUNT(*) > 1

--Data Integration--
--Join tables to combine information--
select sales_data.t_transaction_id, products_data.p_product_name, customer_data.c_customer_name, store_data.s_store_location, sales_data.r_revenue, sales_data.t_transaction_date
from sales_data
join products_data ON sales_data.p_product_id = products_data.p_product_id
join customer_data ON sales_data.c_customer_id = customer_data.c_customer_id
join store_data ON sales_data.s_store_id = store_data.s_store_id;

 Data Analysis & Findings
The following SQL queries were developed to answer specific business questions:
1.	Write a SQL query to retrieve all columns for sales
--Total revenue per product--
select products_data.p_product_name, sum(sales_cleaned_data.r_revenue) AS total_revenue
from sales_cleaned_data
join products_data on sales_cleaned_data.p_product_id = products_data.p_product_id
group by products_data.p_product_name
order by total_revenue desc;

--Total revenue per customer--
select customer_data.c_customer_name, sum(sales_cleaned_data.r_revenue) AS total_revenue
from sales_cleaned_data
join customer_data on sales_cleaned_data.c_customer_id = customer_data.c_customer_id
group by customer_data.c_customer_name
order by total_revenue desc;

--Total revenue per store--
select store_data.s_store_location, sum(sales_cleaned_data.r_revenue) AS total_revenue
from sales_cleaned_data
join store_data on sales_cleaned_data.s_store_id = store_data.s_store_id
group by store_data.s_store_location
order by total_revenue desc;

-- Maximum and Minimum revenue per transaction--
select max(r_revenue) as max_revenue, min(r_revenue) as min_revenue
from sales_cleaned_data;

--Average quantity Sold per Transaction--
select avg(q_quantity) as average_quantity_sold
from sales_cleaned_data;
----
Dashboard Report on Power Bi 
Connect dataset retail sales data company to implement the data analytical technique and also visualize the company data.
•	Sales Summary: A detailed report summarizing total sales, customer demographics, and category performance.
•	Trend Analysis: Insights into sales trends across different months and shifts.
•	Customer Insights: Reports on top customers and unique customer counts per category.
•	Tools:
•	Power BI
•	Sales Summary: A detailed report summarizing total sales, customer demographics, and category performance.
•	Trend Analysis: Insights into sales trends across different months and shifts.
•	Customer Insights: Reports on top customers and unique customer counts per category.

	Conclusion
This project serves as a comprehensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.
