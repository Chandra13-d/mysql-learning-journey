# 📘 DDL & DML in MySQL

## 🔹 What is DDL (Data Definition Language)?
DDL (Data Definition Language) is used to **define, create, and manage the structure** of database objects such as tables, schemas, views, and indexes.

✅ Characteristics:
- Auto-committed (changes are permanent immediately).
- Deals with schema/structure, not actual data.
- Commands: **CREATE, ALTER, DROP, TRUNCATE**

## 🔹 What is DML (Data Manipulation Language)?
DML (Data Manipulation Language) is used to **insert, update, delete, and retrieve data** inside database tables.

✅ Characteristics:
- Not auto-committed (can be rolled back).
- Deals with actual **data stored inside tables**.
- Commands: **INSERT, UPDATE, DELETE, SELECT**

```
### ER Diagram ( Real-World Example: E commerce Database)  
📌 ER Modeling in DBMS

ER (Entity–Relationship) modeling is a high-level conceptual design of a database. 
It helps visualize how entities (things), relationships (connections), and attributes (properties) are structured before
 we actually create tables in SQL.

🔹 1. Entity: An Entity represents a real-world object that can be stored in the database.
              It can be tangible (Customer, Product) or intangible (Order, Payment).
              In ER diagrams, entities are shown as rectangles.

👉 E-commerce Example:
 Entities could be:     Customer
                        Product
                        Order
                        Payment
                        Cart

🔹 2. Attribute: An Attribute describes the properties or details of an entity.
                  Shown as ovals connected to their entity.

Types of attributes:
                Simple: indivisible (e.g., name, price)
                Composite: can be divided (e.g., full_name → first_name + last_name)
                Derived: can be calculated (e.g., age from birthdate)
                Multivalued: multiple values allowed (e.g., phone_numbers)

👉 E-commerce Example:
                Customer: customer_id, name, email, phone
                Product: product_id, product_name, price, stock_qty
                Order: order_id, order_date, total_amount

🔹 3. Relationship: A Relationship shows how two or more entities are connected.
                    Shown as diamonds in ER diagrams.

  Types:
        One-to-One (1:1): A passport belongs to one person.
        One-to-Many (1:N): A customer can place many orders, but each order belongs to one customer.
        Many-to-Many (M:N): A product can appear in many orders, and an order can have many products.

👉 E-commerce Example:
                    A Customer places an Order (1:N relationship).
                    An Order contains Products (M:N relationship).
                    A Payment is made for an Order (1:1 relationship).

🔹 4. Keys in ER Model
            Primary Key: Unique identifier for an entity (e.g., customer_id). 
                    It ensures that each row has a unique identifier and no duplicate values are allowed.
                    It serves as a reference for establishing relationships between tables.
                    Each table can have only one primary key.
            Foreign Key: A foreign key is a field in a table that is used to establish a link between the data in two tables.
                    It creates a relationship between the foreign key field in one table and the primary key in another table.
            Unique Key: A unique key ensures that the values in the specified column(s) are unique across all rows in the table.
                    Unlike the primary key, a table can have multiple unique keys.


🔹 5. E-Commerce ER Diagram (Conceptual)
Here’s a text description (imagine boxes and diamonds in ER diagram form):

Customer (customer_id, name, email, phone)
⬇️ places (1:N)
Order (order_id, order_date, total_amount, customer_id)
⬇️ contains (M:N)
Product (product_id, product_name, price, stock_qty)
⬇️ belongs_to (1:1)
Payment (payment_id, payment_method, amount, order_id) 
``` 
--------------------------------------------------------------------------------------
## 🛒 Real-World Example 2: E-Commerce Database
**ER Diagram (E-Commerce)**
```sql
    CUSTOMERS {
        int customer_id PK
        varchar name
        varchar email
        varchar city
    }
    ORDERS {
        int order_id PK
        date order_date
        int customer_id FK
        decimal total_amount
    }
    PRODUCTS {
        int product_id PK
        varchar product_name
        decimal price
    }
    ORDER_ITEMS {
        int order_item_id PK
        int order_id FK
        int product_id FK
        int quantity
    }
-----------------------------------------------------------------------------------------
DDL Examples (E-Commerce)

-- Create Customers table
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    email VARCHAR(100) UNIQUE,
    city VARCHAR(50)
);

-- Create Orders table
CREATE TABLE Orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    order_date DATE,
    customer_id INT,
    total_amount DECIMAL(10,2),
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);

-- Alter: Add phone number column to Customers
ALTER TABLE Customers ADD phone_number VARCHAR(15);
--------------------------------------------------------------------------------
DML Examples (E-Commerce)

-- Insert a customer
INSERT INTO Customers (name, email, city, phone_number) 
VALUES ('Anita Sharma', 'anita@gmail.com', 'Delhi', '9998887777');

-- Insert an order
INSERT INTO Orders (order_date, customer_id, total_amount) 
VALUES ('2025-09-10', 1, 2500.00);

-- Update customer city
UPDATE Customers SET city = 'Mumbai' WHERE customer_id = 1;

-- Delete an order
DELETE FROM Orders WHERE order_id = 1;

-- Select orders with customer name

## Get all customer orders with total amount

SELECT o.order_id, o.total_amount, c.name
FROM Orders o
JOIN Customers c ON o.customer_id = c.customer_id;

Output

|  order_id | name  | total_amount  |
| --------- | ----- | ------------- |
| 101       | Alice | 5000.00       |
| 102       | Bob   | 3000.00       |

## Get products bought in each order

SELECT o.order_id, c.name, p.product_name, oi.quantity
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
JOIN order_items oi ON o.order_id = oi.order_id
JOIN products p ON oi.product_id = p.product_id;

Output

| order_id  | name  | product_name    | quantity |
| --------- | ----- | --------------- | -------- |
| 101       | Alice | Gold Ring       | 2        |
| 101       | Alice | Diamond Earring | 1        |
| 102       | Bob   | Silver Necklace | 3        |

--------------------------------------------------------------------------------------

``` ``
## 🔑 Key Difference Between DDL & DML
Feature	DDL	DML
Purpose	Defines database structure	Manipulates the data inside the tables
Examples	CREATE, ALTER, DROP, TRUNCATE	INSERT, UPDATE, DELETE, SELECT
Auto Commit	Yes (permanent immediately)	No (can ROLLBACK changes)

✅ Summary:

DDL defines and manages the database structure.
DML is used to insert, modify, delete, and retrieve data.
Together, they form the foundation of working with databases in MySQL.

````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````
