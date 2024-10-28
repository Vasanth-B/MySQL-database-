# E-commerce Database System

## Overview

This project sets up a foundational e-commerce database using MySQL to manage customers, products, orders, and individual order items. The database supports common e-commerce functionality, including storing customer and product information, processing orders, and handling order details, such as quantities and pricing. The schema is designed for efficiency and scalability, with normalized tables to reduce redundancy and improve data integrity.

---

## Key Features

- **Customer Management:** Stores essential customer information, including name, email, and address.
- **Product Catalog:** Manages products with details like name, price, description, and optional discounts.
- **Order Processing:** Tracks each order, including the customer, date, and total order amount.
- **Order Item Details:** Supports multiple products per order, tracking quantities and purchase price.
- **Data Retrieval & Analysis:** SQL queries for extracting insights, such as recent orders, customer spending, and top-selling products.
- **Updatable Product Pricing & Discounts:** Enables adjustments to product prices and the addition of discounts.

---

## Database Schema

The database includes the following tables:

### 1. `customers`
- **Columns:**  
  - `id` (INT): Primary key, auto-incremented  
  - `name` (VARCHAR): Customer's name  
  - `email` (VARCHAR): Unique customer email  
  - `address` (VARCHAR): Customer's address  

### 2. `products`
- **Columns:**  
  - `id` (INT): Primary key, auto-incremented  
  - `name` (VARCHAR): Product name  
  - `price` (DECIMAL): Product price  
  - `description` (TEXT): Product description  
  - `discount` (DECIMAL): Optional discount on the product  

### 3. `orders`
- **Columns:**  
  - `id` (INT): Primary key, auto-incremented  
  - `customer_id` (INT): Foreign key referencing `customers(id)`  
  - `order_date` (DATE): Date of order placement  
  - `total_amount` (DECIMAL): Calculated total order amount  

### 4. `order_items`
- **Columns:**  
  - `id` (INT): Primary key, auto-incremented  
  - `order_id` (INT): Foreign key referencing `orders(id)`  
  - `product_id` (INT): Foreign key referencing `products(id)`  
  - `quantity` (INT): Quantity of product in the order  
  - `price` (DECIMAL): Product price at purchase  

---

## Example SQL Queries

Here are some useful SQL queries for data management and analysis:

1. **Retrieve all customers with orders in the last 30 days:**
    ```sql
    SELECT customers.name, customers.email
    FROM customers
    JOIN orders ON customers.id = orders.customer_id
    WHERE order_date >= CURDATE() - INTERVAL 30 DAY;
    ```

2. **Get total spending by each customer:**
    ```sql
    SELECT customers.name, SUM(orders.total_amount) AS total_spent
    FROM customers
    JOIN orders ON customers.id = orders.customer_id
    GROUP BY customers.name;
    ```

3. **Update the price of a specific product (e.g., Product C) to 45.00:**
    ```sql
    UPDATE products
    SET price = 45.00
    WHERE name = 'Product C';
    ```

4. **Add a `discount` column to the `products` table:**
    ```sql
    ALTER TABLE products
    ADD COLUMN discount DECIMAL(5, 2) DEFAULT 0.00;
    ```

5. **Retrieve the top 3 most expensive products:**
    ```sql
    SELECT name, price
    FROM products
    ORDER BY price DESC
    LIMIT 3;
    ```

---

## Getting Started

1. **Database Setup:** Set up MySQL and create a new database for the e-commerce system.
2. **Table Creation:** Use the SQL commands provided to create the `customers`, `products`, `orders`, and `order_items` tables.
3. **Data Insertion:** Populate the tables with sample data for testing (optional).
4. **Run Queries:** Use the example SQL queries to retrieve and analyze data.

---