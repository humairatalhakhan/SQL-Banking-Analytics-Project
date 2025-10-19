# 💾 SQL Banking Analytics

An **SQL Server banking analytics project** analyzing customer deposits, accounts, and transaction activities.  
Turn raw banking data into actionable insights using **SQL queries, relational tables, and trend analysis**.

<img width="952" height="936" alt="SQL Screen" src="https://github.com/user-attachments/assets/124f7f6a-a3c1-479f-af3d-3924a605bbd9" />

---

## 📊 Project Overview

This project simulates **real-world banking scenarios**, helping to track:

- Customer deposits, withdrawals, and balances  
- Branch performance  
- Transaction trends over time  
- Data cleaning and KPI calculation  

It includes three main tables: **Customers**, **Accounts**, and **Transactions**, along with **sample data** and **ready-to-run SQL queries**.

---

## ⚙️ Database Schema

### **Customers**
| Column        | Type       | Description                     |
|---------------|------------|---------------------------------|
| CustomerID    | VARCHAR(10)| Unique customer identifier      |
| CustomerName  | VARCHAR(50)| Customer full name              |
| AccountType   | VARCHAR(20)| Individual or Corporate         |
| Branch        | VARCHAR(50)| Branch location                 |
| JoinDate      | DATE       | Account creation date           |
| Status        | VARCHAR(20)| Active / Inactive               |

### **Accounts**
| Column          | Type        | Description                        |
|-----------------|------------|-----------------------------------|
| AccountID       | VARCHAR(10)| Unique account identifier          |
| CustomerID      | VARCHAR(10)| Linked to Customers table          |
| AccountType     | VARCHAR(20)| Savings / Current                  |
| OpeningBalance  | DECIMAL    | Initial deposit                    |
| CurrentBalance  | DECIMAL    | Current account balance            |
| LastTransactionDate | DATE    | Most recent transaction            |

### **Transactions**
| Column        | Type       | Description                       |
|---------------|------------|----------------------------------|
| TransactionID | VARCHAR(10)| Unique transaction identifier    |
| AccountID     | VARCHAR(10)| Linked to Accounts table         |
| TransactionDate | DATE     | Date of transaction              |
| Type          | VARCHAR(20)| Deposit / Withdrawal             |
| Amount        | DECIMAL    | Transaction amount               |
| Channel       | VARCHAR(20)| ATM / Online / Branch            |

---
###🚀 Project Features

Relational database design with foreign keys

Sample data covering deposits, withdrawals, and account balances

SQL queries for trend analysis, performance comparison, and KPI calculation

Clean, reusable, and scalable database for banking analytics

🛠 Tools & Technologies
Tool	Purpose
SQL Server	Database creation & querying

## 👩‍💻 About the Author

**Humaira Talha Khan**  
Business Coordinator | Banking Analytics Enthusiast  
Passionate about turning financial data into actionable business insights.  

🔗 **Connect with me:**  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/humairatalha/)  
[![GitHub](https://img.shields.io/badge/GitHub-000?style=for-the-badge&logo=github&logoColor=white)](https://humairatalhakhan.github.io//)


🎯 Next Steps:

Clone this repository.

Execute the SQL scripts in SQL Server Management Studio.

Run the provided queries to explore analytics insights.

Extend the project with more transactions, customers, or advanced analytics.

## 📌 Example SQL Queries

**1️⃣ Total deposits & withdrawals per customer**
```sql
SELECT 
    c.CustomerName,
    SUM(CASE WHEN t.Type='Deposit' THEN t.Amount ELSE 0 END) AS TotalDeposits,
    SUM(CASE WHEN t.Type='Withdrawal' THEN t.Amount ELSE 0 END) AS TotalWithdrawals
FROM Customers c
JOIN Accounts a ON c.CustomerID = a.CustomerID
JOIN Transactions t ON a.AccountID = t.AccountID
GROUP BY c.CustomerName;
**2️⃣ Current balance per branch
SELECT 
    c.Branch,
    SUM(a.CurrentBalance) AS TotalBalance
FROM Accounts a
JOIN Customers c ON a.CustomerID = c.CustomerID
GROUP BY c.Branch
ORDER BY TotalBalance DESC;
**3️⃣ Top 3 customers by balance
SELECT c.CustomerName, a.CurrentBalance
FROM Accounts a
JOIN Customers c ON a.CustomerID = c.CustomerID
ORDER BY a.CurrentBalance DESC
OFFSET 0 ROWS FETCH NEXT 3 ROWS ONLY;
**4️⃣ Monthly transaction trend
SELECT 
    FORMAT(TransactionDate, 'yyyy-MM') AS Month,
    COUNT(*) AS TotalTransactions,
    SUM(Amount) AS TotalAmount
FROM Transactions
GROUP BY FORMAT(TransactionDate, 'yyyy-MM')
ORDER BY Month;



