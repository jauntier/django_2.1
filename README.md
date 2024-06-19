# django_2.1
The postgresql code for the first challenge is as follows.

CREATE DATABASE small_company;


\c small_company;


CREATE TABLE departments (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    manager_id INT
);

CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    email VARCHAR(100),
    phone_number VARCHAR(20),
    department_id INT REFERENCES departments(id)
);

CREATE TABLE projects (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    description TEXT,
    start_date DATE,
    end_date DATE
);


INSERT INTO departments (name, manager_id) VALUES
('HR', 1),
('Engineering', 2);

INSERT INTO employees (first_name, last_name, email, phone_number, department_id) VALUES
('John', 'Doe', 'john.doe@example.com', '555-1234', 1),
('Jane', 'Smith', 'jane.smith@example.com', '555-5678', 2);

INSERT INTO projects (name, description, start_date, end_date) VALUES
('Project Alpha', 'Description of Project Alpha', '2024-01-01', '2024-06-30'),
('Project Beta', 'Description of Project Beta', '2024-02-01', '2024-07-31');


ALTER TABLE employees ADD COLUMN job_title VARCHAR(100);

DROP TABLE projects;

ALTER TABLE departments DROP COLUMN manager_id;







The postgresql code for the second challenge is as follows.


CREATE DATABASE online_bookstore;


\c online_bookstore;


CREATE TABLE authors (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    biography TEXT,
    website VARCHAR(100)
);

CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    title VARCHAR(100),
    description TEXT,
    price DECIMAL(10, 2),
    publication_date DATE,
    author_id INT REFERENCES authors(id)
);

CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    email VARCHAR(100),
    password VARCHAR(100),
    phone_number VARCHAR(20),
    address VARCHAR(255)
);

CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    customer_id INT REFERENCES customers(id),
    book_id INT REFERENCES books(id),
    quantity INT,
    order_date DATE
);


SELECT books.title, authors.name
FROM books
JOIN authors ON books.author_id = authors.id;


SELECT customers.first_name, customers.last_name, orders.id AS order_id, orders.order_date, orders.quantity, books.title
FROM customers
JOIN orders ON customers.id = orders.customer_id
JOIN books ON orders.book_id = books.id;


SELECT books.title, SUM(orders.quantity) AS total_sold
FROM orders
JOIN books ON orders.book_id = books.id
GROUP BY books.title
ORDER BY total_sold DESC
LIMIT 5;


SELECT SUM(orders.quantity * books.price) AS total_revenue
FROM orders
JOIN books ON orders.book_id = books.id;


SELECT customers.first_name, customers.last_name, COUNT(orders.id) AS total_orders
FROM customers
JOIN orders ON customers.id = orders.customer_id
GROUP BY customers.id
ORDER BY total_orders DESC
LIMIT 1;


The postgresql code for the first challenge is as follows.
