# SQL Task


## Create Database

```sql
CREATE DATABASE ECOMMERCE;
```
## Use Database

```sql
USE ECOMMERCE;
```

## Create Tables

### Create customers table

```sql
CREATE TABLE CUSTOMERS (
    ID INT PRIMARY KEY AUTO_INCREMENT UNIQUE,
    Name VARCHAR(100),
    Email VARCHAR(100) UNIQUE,
    Address VARCHAR(250)
);
```

### Create orders table

```sql
CREATE TABLE ORDERS (
    ID INT PRIMARY KEY AUTO_INCREMENT UNIQUE,
    CUSTOMER_ID INT,
    ORDER_DATE DATE,
    TOTAL_AMOUNT DECIMAL(10,2),
    FOREIGN KEY (CUSTOMER_ID) REFERENCES CUSTOMERS(ID)
);
```

### Create products table

```sql
CREATE TABLE PRODUCTS (
    ID INT PRIMARY KEY AUTO_INCREMENT UNIQUE,
    Name VARCHAR(100),
    Price DECIMAL(10,2),
    Description TEXT
);
```

## SHOW TABLE 

```sql
SHOW TABLES;
```

## INSERT DATA 

### INSERT DATA INTO CUSTOMER TABLE

```sql
INSERT INTO CUSTOMERS(Name, email, address) VALUES
('Alice', 'alice@example.com','123 Main St,New York'),
('John', 'john@example.com', '234 West St, India'),
('David', 'david@example.com', '345 South St, UK');
```

### INSERT DATA INTO PRODUCTS TABLE

```sql
INSERT INTO PRODUCTS (name, price, description) VALUES
('Product A', 25.00, 'Basic product A'),
('Product B', 40.00, 'Premium product B'),
('Product C', 50.00, 'Exclusive product C'),
('Product D', 75.00, 'Luxury product D');
```

### INSERT DATA INTO ORDERS TABLE

```sql
INSERT INTO ORDERS (customer_id, order_date, total_amount) VALUES
(1, CURDATE() - INTERVAL 5 DAY, 120.00),
(2, CURDATE() - INTERVAL 31 DAY, 200.00),
(1, CURDATE() - INTERVAL 40 DAY, 80.00),
(3, CURDATE() - INTERVAL 2 DAY, 300.00);
```


## QUERIES TO WRITE:

### Retrieve all customers who have placed an order in the last 30 days.

```sql
SELECT DISTINCT c.*
FROM customers c
JOIN orders o ON c.id = o.customer_id
WHERE o.order_date >= CURDATE() - INTERVAL 30 DAY;
```

### Get the total amount of all orders placed by each customer.

```sql
SELECT c.name, SUM(o.total_amount) AS total_spent
FROM customers c
JOIN orders o ON c.id = o.customer_id
GROUP BY c.id, c.name;
```

### Update the price of Product C to 45.00.

```sql
UPDATE Products
SET Price = 45
WHERE Price = 50;
```

### Add a new column discount to the products table.

```sql
ALTER TABLE Products
ADD COLUMN discount DECIMAL(10,2);
```

### Retrieve the top 3 products with the highest price.

```sql 
SELECT * 
from products
ORDER BY price DESC
LIMIT 3;
```

### Get the names of customers who have ordered Product A.

#### Alter orders table with product id as a foreign key

```sql
ALTER TABLE Orders
ADD COLUMN product_id INT,
ADD FOREIGN KEY (product_id) REFERENCES products(id);
```