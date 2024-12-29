SQL Script for Database and Tables Creation

Create the database

  CREATE DATABASE ecommerce;

Use the database

   USE ecommerce;

Create the customers table

   CREATE TABLE customers ( id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL, address TEXT );

Create the products table

    CREATE TABLE products ( id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(255) NOT NULL, 
     price DECIMAL(10, 2) NOT NULL, description TEXT );

Create the orders table

    CREATE TABLE orders ( id INT AUTO_INCREMENT PRIMARY KEY, customer_id INT NOT NULL, order_date DATE 
    NOT NULL, total_amount DECIMAL(10, 2) NOT NULL, FOREIGN KEY (customer_id) REFERENCES customers(id) );

Insert sample data into customers

     INSERT INTO customers (name, email, address) VALUES ('Subadevi','suba@example.com', '123 
     tv Street'), ('harish', 'harish@example.com', '255 main road'), ('priya', 'priya@example.com', '244 cross street');

Insert sample data into products

      INSERT INTO products (name, price, description) VALUES ('Washng machine', 25000, 
     'super fast'), ('Fastrack watch', 4000, '1 year warenty), ('LG tv', 20000, 'smart tv');

Insert sample data into orders

      INSERT INTO orders (customer_id, order_date, total_amount) VALUES (11, '2024-12-19', 10000.00),
      (12, '2024-12-20', 2000.00), (13, '2024-11-18', 500.00);

Retrieve all customers who have placed an order in the last 30 days:

      SELECT DISTINCT c.name, c.email FROM customers c JOIN orders o ON c.id = o.customer_id WHERE
      o.order_date > CURDATE() - INTERVAL 30 DAY;

Get the total amount of all orders placed by each customer:

     SELECT c.name, SUM(o.total_amount) AS total_spent FROM customers c JOIN orders o ON 
     c.id = o.customer_id GROUP BY c.name;

Update the price of LG TV to 20000.00:

    UPDATE products SET price = 20000.00 WHERE name = 'LG tv';

Add a new column discount to the products table:

    ALTER TABLE products ADD COLUMN discount DECIMAL(5, 2) DEFAULT 0.00;

Retrieve the top 3 products with the highest price:

   SELECT name, price FROM products ORDER BY price DESC LIMIT 3;

