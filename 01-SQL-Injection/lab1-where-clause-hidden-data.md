# Lab: SQL Injection in WHERE Clause (Hidden Data Retrieval)

## 🧩 Vulnerability
SQL Injection

## 🎯 Objective
Retrieve hidden/unreleased products by exploiting SQL injection in a WHERE clause.

## 🔍 Entry Point
Product category filter parameter in URL

## 💣 Payload Used
' OR 1=1--

## ⚙️ Steps
1. Open the product category page
2. Observe the URL parameter (e.g., category=Gifts)
3. Modify the parameter:
   category=Gifts' OR 1=1--
4. All products, including hidden ones, are displayed

## 🧠 Why It Worked
The application included user input directly in the SQL query:

SELECT * FROM products WHERE category = 'Gifts' AND released = 1

After injection:

SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1

- `OR 1=1` makes the condition always true  
- `--` comments out the rest of the query  

This bypasses the restriction and returns all data.

## 🛡️ Fix
- Use parameterized queries (prepared statements)
- Sanitize and validate user input
- Avoid directly embedding user input in SQL queries

## 🔗 Platform
PortSwigger Web Security Academy
