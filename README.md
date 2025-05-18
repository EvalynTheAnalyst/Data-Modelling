# E-commerce Data Modelling

## Introduction ##
This repository showcases a robust and scalable data model designed to power analytics and reporting for eCommerce platforms. The goal is to transform raw transactional and operational data into meaningful insights that support smarter business decisions.

---

## Project Overview

In the fast-moving world of eCommerce, accurate data modeling is essential for efficient operations and growth. This project focuses on:

- Building a star schema to support analytics across  order, customers,suppliers, date and product.

---
## Real-World Benefits
 Faster Queries: Well-modeled data reduces response times.

 Accurate Insights: Clear relationships make reporting more precise.

 Data Integrity: Foreign key constraints reduce data entry errors.

 Scalability: Easy to add features like discounts, reviews, or shipping tracking later. 


## Data Model Highlights

- **Fact Tables**:
  - `fact_order`: Central order  transactions table
  - `fact_inventory`: Daily stock levels and movement

- **Dimension Tables**:
  - `dim_customers`: Customer profiles and segmentation
  - `dim_products`: Product catalog with categories and pricing
  - `dim_date`: Calendar table for flexible time-based analysis
  - `dim-payment` : Checl transaction history
 

---

## Tool Used:

- **SQL** (PostgreSQL / MySQL for modeling and querying)  
- **drawSQL** (to show relationship and data modelling)

## Relationships##


![image](https://github.com/user-attachments/assets/96ac27dc-c2af-4430-ab41-7e99604fa9e5)

## Table Creation and Results ##
**Create schema** 
``` CREATE SCHEMA ecommerce;  
SET search_path TO ecommerce;   

#### Create customers table
CREATE TABLE customers (
 customer_id SERIAL PRIMARY KEY,
 name VARCHAR(100),
 email VARCHAR(100),
 phone_number VARCHAR(100),
 locations VARCHAR(100)
);


#### Create products table
 CREATE TABLE products (
 product_id SERIAL PRIMARY KEY,
 product_name VARCHAR(100),
 product_category VARCHAR(100),
product_price FLOAT
);

 #### Create transactions table
CREATE TABLE transactions (
  transaction_id SERIAL PRIMARY KEY,
  transaction_type VARCHAR(100),
  transaction_date DATE
);

#### Create orders table
 CREATE TABLE orders (
  order_id SERIAL PRIMARY KEY,
  order_date DATE,
  customer_id INT REFERENCES customers(customer_id),
  product_id INT REFERENCES products(product_id),
  transaction_id INT REFERENCES transactions(transaction_id),
  quantity INT,
  sales NUMERIC(8,2)
);

#### Insert data into customers
 INSERT INTO customers (name, email, phone_number, locations) VALUES
 ('Alice Mwangi', 'alice@example.com', '0712345678', 'Nairobi'),
 ('Brian Otieno', 'brian@example.com', '0723456789', 'Kisumu'),
 ('Cynthia Wanja', 'cynthia@example.com', '0734567890', 'Mombasa');

-- Insert data into products
INSERT INTO products (product_id, product_name, product_category, product_price) VALUES
(101, 'Wireless Mouse', 'Electronics', 1500.00),
(102, 'Bluetooth Speaker', 'Electronics', 3000.00),
(103, 'Office Chair', 'Furniture', 7500.00);

-- Insert data into transactions
INSERT INTO transactions (transaction_id, transaction_type, transaction_date) VALUES
 (1001, 'Credit Card', '2025-05-15'),
 (1002, 'Mpesa', '2025-05-16'),
 (1003, 'PayPal', '2025-05-17');

-- Insert data into orders
INSERT INTO orders (order_id, order_date, customer_id, product_id, transaction_id, quantity, sales) VALUES
(5001, '2025-05-15', 1, 101, 1001, 2, 3000.00),
(5002, '2025-05-16', 2, 102, 1002, 1, 3000.00),
(5003, '2025-05-17', 3, 103, 1003, 1, 7500.00);
 ``` 

     
-- Sample queries

``` SELECT * FROM customers; ```

![image](https://github.com/user-attachments/assets/ed154717-332d-4176-9bb4-016fdc0a0155)

``` SELECT * FROM orders; ```

![image](https://github.com/user-attachments/assets/a11cf3d4-11e5-470e-a34a-bcdca779c8e0)











