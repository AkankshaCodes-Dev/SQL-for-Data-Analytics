# SQL Day 7 — Revision & Practice Checkpoint

![SQL](https://img.shields.io/badge/SQL-Practice-blue)
![Day](https://img.shields.io/badge/Day-07-purple)
![Status](https://img.shields.io/badge/Status-Completed-success)

## 📌 About This Day

Day 7 was dedicated to revising the SQL concepts I learned during Days 1–6 and testing my understanding through a practical checkpoint.

I worked with an `employees` table containing 15 employee records and practiced retrieving, filtering, sorting, counting, and analyzing employee data using SQL queries.

**Day 7 Goal:** Revise SQL fundamentals and solve 15 mixed practice questions independently.

## 🎯 Learning Objectives

- Revise basic SQL syntax.
- Retrieve specific columns and complete records.
- Filter data using `WHERE`.
- Retrieve unique values using `DISTINCT`.
- Sort records using `ORDER BY`.
- Use aggregate functions to analyze data.
- Group records using `GROUP BY`.
- Filter grouped results using `HAVING`.
- Practice writing SQL queries independently.

## 🗂️ Dataset: Employees

The `employees` table contains five columns and 15 employee records.

### Table Structure

| Column Name | Data Type | Description |
|---|---|---|
| `employee_id` | INT | Unique employee ID |
| `employee_name` | VARCHAR(50) | Employee name |
| `department` | VARCHAR(30) | Employee department |
| `city` | VARCHAR(30) | Employee city |
| `salary` | INT | Employee salary |

### Employees Table Data

| employee_id | employee_name | department | city | salary |
|---:|---|---|---|---:|
| 101 | Anu | IT | Ballari | 30000 |
| 102 | Ravi | Sales | Bengaluru | 35000 |
| 103 | Priya | IT | Ballari | 40000 |
| 104 | Kiran | HR | Mysuru | 25000 |
| 105 | Meena | Sales | Bengaluru | 30000 |
| 106 | Arjun | IT | Mysuru | 45000 |
| 107 | Divya | HR | Ballari | 28000 |
| 108 | Suresh | Sales | Mysuru | 32000 |
| 109 | Neha | IT | Bengaluru | 38000 |
| 110 | Rahul | Finance | Ballari | 42000 |
| 111 | Sneha | Finance | Bengaluru | 40000 |
| 112 | Vikram | IT | Mysuru | 50000 |
| 113 | Pooja | Sales | Ballari | 27000 |
| 114 | Manish | HR | Bengaluru | 26000 |
| 115 | Kavya | Finance | Mysuru | 45000 |

## 📝 Day 7 — All 15 Practice Questions

### Part 1: Data Retrieval and Filtering

**Q1. Display all columns and all records from the `employees` table.**

Concept: `SELECT *`

**Q2. Display only the employee names and their salaries.**

Concept: Selecting specific columns.

**Q3. Display employees who work in the IT department.**

Concept: `WHERE`

**Q4. Display employees whose salary is greater than 35,000.**

Concept: `WHERE` with a comparison operator.

**Q5. Display employees who live in Ballari.**

Concept: Filtering text values using `WHERE`.

**Q6. Display all unique departments available in the table.**

Concept: `DISTINCT`

### Part 2: Sorting and Aggregate Functions

**Q7. Display employees in ascending order of salary.**

Concept: `ORDER BY ASC`

**Q8. Display employees in descending order of salary.**

Concept: `ORDER BY DESC`

**Q9. Count the total number of employees and display the result with the alias `Total_Employees`.**

Concept: `COUNT()` and `AS`

**Q10. Calculate the total salary of all employees.**

Concept: `SUM()`

**Q11. Calculate the average salary of all employees.**

Concept: `AVG()`

**Q12. Find the minimum and maximum salaries in the employees table.**

Concept: `MIN()` and `MAX()`

### Part 3: Grouping and Group Filtering

**Q13. Calculate the total salary for each department.**

Concept: `GROUP BY` and `SUM()`

**Q14. Count the number of employees in each department.**

Concept: `GROUP BY` and `COUNT()`

**Q15. Display departments whose total salary is greater than 100,000.**

Concept: `GROUP BY`, `SUM()` and `HAVING`

## 💻 Sample SQL Solutions

These examples demonstrate some of the concepts practiced during the checkpoint.

### 1. Retrieve All Employees

```sql
SELECT *
FROM employees;
```

### 2. Filter IT Department Employees

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

### 3. Sort Employees by Salary

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

### 4. Calculate Department-Wise Total Salary

```sql
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

### 5. Find Departments with Total Salary Above 100,000

```sql
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department
HAVING SUM(salary) > 100000;
```

## 📚 SQL Concepts Revised

| SQL Concept | Purpose |
|---|---|
| `SELECT` | Retrieve data |
| `WHERE` | Filter individual records |
| `DISTINCT` | Retrieve unique values |
| `ORDER BY` | Sort records |
| `COUNT()` | Count records |
| `SUM()` | Calculate totals |
| `AVG()` | Calculate averages |
| `MIN()` | Find the minimum value |
| `MAX()` | Find the maximum value |
| `AS` | Assign an alias |
| `GROUP BY` | Group records |
| `HAVING` | Filter grouped results |

## 🔍 Important Learning

### Difference Between WHERE and HAVING

- `WHERE` filters individual rows before grouping.
- `HAVING` filters groups after `GROUP BY`.

Example:

```sql
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department
HAVING SUM(salary) > 100000;
```

This query groups employees by department, calculates the total salary for each department, and returns only departments whose total exceeds 100,000.

## ✅ Day 7 Checkpoint Results

| Metric | Result |
|---|---|
| Total employee records | 15 |
| Total practice questions | 15 |
| Questions completed | 15/15 |
| Revision checkpoint | Completed |
| Learning focus | SQL fundamentals |
| Next step | Continue SQL practice |

## 🚀 Key Takeaways

- Strengthened my understanding of SQL fundamentals.
- Practiced filtering and sorting employee records.
- Applied aggregate functions to calculate salary statistics.
- Practiced department-wise analysis using `GROUP BY`.
- Revised the difference between `WHERE` and `HAVING`.
- Completed a 15-question SQL revision checkpoint.

## 📅 Learning Journey

**Day 7 of my SQL learning journey — Revision and Practice.**

This checkpoint helped me review the concepts I had learned so far and build confidence in writing SQL queries independently.

I will continue practicing SQL and gradually move toward more advanced data analysis queries.

---

**Skills:** SQL Fundamentals | Data Filtering | Sorting | Aggregate Functions | Grouping | Data Analysis

**#SQL #DataAnalytics #SQLPractice #LearningJourney #100DaysOfCode**
