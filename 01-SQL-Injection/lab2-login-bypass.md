# Lab: SQL Injection Login Bypass

## 🧩 Vulnerability
SQL Injection

## 🎯 Objective
Bypass authentication and log in as a valid user without knowing credentials.

## 🔍 Entry Point
Login form (username and password fields)

## 💣 Payload Used
' OR 1=1--

## ⚙️ Steps
1. Open the login page
2. Enter the following payload:
   - Username: ' OR 1=1--
   - Password: anything
3. Submit the request
4. Login is successful without valid credentials

## 🧠 Why It Worked
The application constructed a SQL query like:

SELECT * FROM users WHERE username = 'input' AND password = 'input'

After injection:

SELECT * FROM users WHERE username = '' OR 1=1--' AND password = 'anything'

- `OR 1=1` makes the condition always true  
- `--` comments out the rest of the query  

This allows authentication without valid credentials.

## 🧪 Testing Approach
- Tried single quote (') to check for SQL behavior
- Confirmed input is not sanitized
- Used logical condition to bypass authentication

## 🛡️ Fix
- Use parameterized queries (prepared statements)
- Implement proper input validation
- Use secure authentication mechanisms

## 🔗 Platform
PortSwigger Web Security Academy
