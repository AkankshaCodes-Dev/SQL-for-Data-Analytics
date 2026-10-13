# 🗄️ Day 1 — SQL Fundamentals

## 📌 Topics Covered
- Introduction to SQL
- Understanding databases and tables
- Rows, columns, and cells
- `SELECT` statement
- `FROM` clause
- Selecting specific columns
- Selecting all columns using `*`

## 📖 What I Learned

SQL stands for Structured Query Language. It is used to communicate with databases and retrieve or manage data.

A database stores organized information, while a table contains related data in rows and columns.

- **Row:** Represents one record.
- **Column:** Represents a field or attribute.
- **SELECT:** Specifies the columns to retrieve.
- **FROM:** Specifies the table from which to retrieve data.

## 💻 SQL Practice

### 1. Retrieve all columns from the Employee table

```sql
SELECT *
FROM Employee;
```

### 2. Retrieve employee names

```sql
SELECT Name
FROM Employee;
```

### 3. Retrieve employee names and departments

```sql
SELECT Name, Department
FROM Employee;
```

## 🧠 Key Takeaways
- `SELECT *` retrieves all columns.
- `SELECT Name` retrieves only the Name column.
- Multiple columns can be selected by separating their names with commas.
- SQL queries help retrieve specific information from a database.

## 🛠️ Learning Resources
- [W3Schools SQL Introduction](https://www.w3schools.com/sql/sql_intro.asp)
- [W3Schools SQL SELECT](https://www.w3schools.com/sql/sql_select.asp)
- [SQL Practice Editor](https://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all)

## 🎯 Next Step
Continue learning SQL and practise retrieving data from tables.

📈 This repository documents my progress as I build my Data Analytics skills one day at a time.

#SQL #DataAnalytics #LearningJourney
