# SQL Constraints Project — CHECK, DEFAULT & UNIQUE

## 📌 Project Overview

This project demonstrates how to use **SQL constraints** to maintain data integrity in relational databases. It focuses on:

* Using **CHECK, DEFAULT, and UNIQUE** constraints
* Validating numeric ranges
* Auto-generating timestamps
* Testing constraint violations
* Understanding constraint enforcement order
* Comparing application vs database validation

---

## 🛠 Technologies Used

* MySQL (or PostgreSQL)
* MySQL Workbench / pgAdmin
* Git & GitHub

---

## 📂 Database Schema & Code

### **1️⃣ Students Table**

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT CHECK (age BETWEEN 18 AND 30),
    email VARCHAR(100) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Valid Insert:

```sql
INSERT INTO students VALUES (1, 'Aman', 22, 'aman@gmail.com', DEFAULT);
```

#### Invalid Insert (CHECK violation):

```sql
INSERT INTO students VALUES (2, 'Riya', 15, 'riya@gmail.com', DEFAULT);
```

---

### **2️⃣ Employees Table**

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    salary INT CHECK (salary >= 10000 AND salary <= 100000)
);
```

#### Valid:

```sql
INSERT INTO employees VALUES (1, 50000);
```

#### Invalid:

```sql
INSERT INTO employees VALUES (2, 500000);
```

---

### **3️⃣ Orders Table (DEFAULT Timestamp)**

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    order_amount INT,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

```sql
INSERT INTO orders (order_id, order_amount)
VALUES (101, 2500);
```

---

### **4️⃣ Products Table (Multiple Constraints)**

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    price INT CHECK (price > 0) DEFAULT 1000
);
```

```sql
INSERT INTO products (product_id) VALUES (1);
```

---
Constraint Enforcement Order (Conceptual)
NOT NULL
CHECK
UNIQUE
DEFAULT
PRIMARY KEY / FOREIGN KEY
Note: Actual enforcement may vary slightly by database engine.
---

Database-Level vs Application-Level Validation
Validation Type	Where	Example
Database-level	SQL constraints	CHECK, UNIQUE
Application-level	Backend code	Regex, form validation
Best Practice
✔ Use both for maximum data safety

---
Constraint Design Decisions
Critical business rules enforced at database level
Prevents invalid data even if application fails
Improves long-term data consistency
Reduces debugging and cleanup effort
---
Final Outcome
---
✅ Intern understands:

Advanced constraint usage
Data validation best practices
Real-world database protection techniques
✅ Database enforces strong data quality and integrity automatically
---
