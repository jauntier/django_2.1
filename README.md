# django_2.1
The postgresql code for it is

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
