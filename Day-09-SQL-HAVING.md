# Day 9 — SQL: HAVING Clause

## 📌 Overview

On Day 9, I learned how to use the SQL `HAVING` clause to filter grouped results. I also practised the difference between `WHERE` and `HAVING` and used aggregate functions such as `AVG()`, `COUNT()`, and `SUM()`.

## 🎯 Learning Objectives

- Understand `WHERE` vs `HAVING`.
- Use `GROUP BY` to group records.
- Filter groups using `HAVING`.
- Apply aggregate functions.
- Combine `WHERE`, `GROUP BY`, `HAVING`, `AND`, and `OR`.
- Practise SQL queries using an employee dataset.

---

## 1. What Is HAVING?

The `HAVING` clause filters groups created using `GROUP BY`.

For example, if we want to find departments whose average salary is greater than ₹35,000, we can use `HAVING`.

### Syntax

```sql
SELECT column_name, AGGREGATE_FUNCTION(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

### Example

```sql
SELECT department, AVG(salary) AS average_salary
FROM Employees
GROUP BY department
HAVING AVG(salary) > 35000;
```

This query returns only departments whose average salary is greater than ₹35,000.

---

## 2. WHERE vs HAVING

| WHERE | HAVING |
|---|---|
| Filters individual rows. | Filters grouped results. |
| Applied before grouping. | Applied after grouping. |
| Commonly filters values such as salary or city. | Commonly filters aggregate results. |
| Does not normally use aggregate functions directly in its condition. | Can filter using `AVG()`, `COUNT()`, and `SUM()`. |

**Remember:**

- `WHERE` = Filters rows.
- `GROUP BY` = Groups rows.
- `HAVING` = Filters groups.

### Simplified SQL Processing Order

1. `FROM`
2. `WHERE`
3. `GROUP BY`
4. `HAVING`
5. `SELECT`
6. `ORDER BY`

This is the logical processing order for the clauses covered here, not necessarily the order in which SQL physically executes operations.

---

## 3. Employee Dataset

The following table is used for all practice queries.

| employee_id | name | department | salary | city |
|---:|---|---|---:|---|
| 1 | Ravi | IT | 40000 | Ballari |
| 2 | Priya | IT | 50000 | Bengaluru |
| 3 | Amit | HR | 25000 | Ballari |
| 4 | Sneha | HR | 35000 | Bengaluru |
| 5 | Rahul | Sales | 30000 | Ballari |
| 6 | Neha | Sales | 40000 | Bengaluru |
| 7 | Kiran | IT | 60000 | Ballari |
| 8 | Pooja | HR | 30000 | Ballari |

### Optional: Create the Table

```sql
CREATE TABLE Employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50),
    department VARCHAR(30),
    salary INT,
    city VARCHAR(50)
);
```

### Insert the Data

```sql
INSERT INTO Employees
(employee_id, name, department, salary, city)
VALUES
(1, 'Ravi', 'IT', 40000, 'Ballari'),
(2, 'Priya', 'IT', 50000, 'Bengaluru'),
(3, 'Amit', 'HR', 25000, 'Ballari'),
(4, 'Sneha', 'HR', 35000, 'Bengaluru'),
(5, 'Rahul', 'Sales', 30000, 'Ballari'),
(6, 'Neha', 'Sales', 40000, 'Bengaluru'),
(7, 'Kiran', 'IT', 60000, 'Ballari'),
(8, 'Pooja', 'HR', 30000, 'Ballari');
```

---

## 4. Aggregate Functions

| Function | Meaning | Example |
|---|---|---|
| `AVG()` | Calculates the average. | `AVG(salary)` |
| `COUNT()` | Counts records. | `COUNT(*)` |
| `SUM()` | Calculates the total. | `SUM(salary)` |

### Example 1: Average Salary by Department

```sql
SELECT department, AVG(salary) AS average_salary
FROM Employees
GROUP BY department;
```

**Expected Output**

| department | average_salary |
|---|---:|
| HR | 30000 |
| IT | 50000 |
| Sales | 35000 |

### Example 2: Departments with Average Salary Above ₹35,000

```sql
SELECT department, AVG(salary) AS average_salary
FROM Employees
GROUP BY department
HAVING AVG(salary) > 35000;
```

**Expected Output**

| department | average_salary |
|---|---:|
| IT | 50000 |

Sales is excluded because its average salary is exactly ₹35,000, not greater than ₹35,000.

### Example 3: Departments with at Least Three Employees

```sql
SELECT department, COUNT(*) AS employee_count
FROM Employees
GROUP BY department
HAVING COUNT(*) >= 3;
```

**Expected Output**

| department | employee_count |
|---|---:|
| HR | 3 |
| IT | 3 |

### Example 4: Departments with Total Salary Above ₹100,000

```sql
SELECT department, SUM(salary) AS total_salary
FROM Employees
GROUP BY department
HAVING SUM(salary) > 100000;
```

**Expected Output**

| department | total_salary |
|---|---:|
| IT | 150000 |

### Example 5: Using WHERE and HAVING Together

```sql
SELECT department, AVG(salary) AS average_salary
FROM Employees
WHERE salary > 30000
GROUP BY department
HAVING AVG(salary) > 35000;
```

**Explanation**

1. `WHERE` filters out employees earning ₹30,000 or less.
2. `GROUP BY` groups the remaining employees by department.
3. `AVG()` calculates the average salary of the remaining employees in each department.
4. `HAVING` keeps groups whose average exceeds ₹35,000.

### Example 6: Using AND

```sql
SELECT department,
       AVG(salary) AS average_salary,
       COUNT(*) AS employee_count
FROM Employees
GROUP BY department
HAVING AVG(salary) > 30000
   AND COUNT(*) >= 3;
```

Both conditions must be true.

### Example 7: Using OR

```sql
SELECT department, AVG(salary) AS average_salary
FROM Employees
GROUP BY department
HAVING AVG(salary) >= 50000
    OR AVG(salary) <= 30000;
```

At least one condition must be true.

---

## 5. SQL Day 9 Practice Questions and Solutions

### Task 1: Find the average salary of each department.

```sql
SELECT department, AVG(salary) AS average_salary
FROM Employees
GROUP BY department;
```

### Task 2: Find departments whose average salary is greater than ₹30,000.

```sql
SELECT department, AVG(salary) AS average_salary
FROM Employees
GROUP BY department
HAVING AVG(salary) > 30000;
```

### Task 3: Find departments that have at least three employees.

```sql
SELECT department, COUNT(*) AS employee_count
FROM Employees
GROUP BY department
HAVING COUNT(*) >= 3;
```

### Task 4: Find departments whose total salary is greater than ₹80,000.

```sql
SELECT department, SUM(salary) AS total_salary
FROM Employees
GROUP BY department
HAVING SUM(salary) > 80000;
```

### Task 5: Find departments whose average salary is greater than or equal to ₹35,000.

```sql
SELECT department, AVG(salary) AS average_salary
FROM Employees
GROUP BY department
HAVING AVG(salary) >= 35000;
```

### Task 6: Find departments with at least two employees earning more than ₹30,000.

```sql
SELECT department, COUNT(*) AS employee_count
FROM Employees
WHERE salary > 30000
GROUP BY department
HAVING COUNT(*) >= 2;
```


| department | employee_count |
|---|---:|
| IT | 3 |

### Task 7: Find departments with average salary above ₹30,000 and at least three employees.

```sql
SELECT department,
       AVG(salary) AS average_salary,
       COUNT(*) AS employee_count
FROM Employees
GROUP BY department
HAVING AVG(salary) > 30000
   AND COUNT(*) >= 3;
```

### Task 8: Find departments whose average salary is less than ₹40,000.

```sql
SELECT department, AVG(salary) AS average_salary
FROM Employees
GROUP BY department
HAVING AVG(salary) < 40000;
```

### Task 9: Find cities with at least four employees.

```sql
SELECT city, COUNT(*) AS employee_count
FROM Employees
GROUP BY city
HAVING COUNT(*) >= 4;
```

**Expected Output**

| city | employee_count |
|---|---:|
| Ballari | 5 |

Bengaluru has three employees, so it does not qualify.

### Task 10: Find departments whose total salary is greater than ₹80,000 OR whose employee count is at least three.

```sql
SELECT department,
       SUM(salary) AS total_salary,
       COUNT(*) AS employee_count
FROM Employees
GROUP BY department
HAVING SUM(salary) > 80000
    OR COUNT(*) >= 3;
```

**Expected Output**

| department | total_salary | employee_count |
|---|---:|---:|
| HR | 90000 | 3 |
| IT | 150000 | 3 |

Sales has total salary of ₹70,000 and two employees, so it does not qualify.

---

## 6. Key Takeaways

- `WHERE` filters individual rows before grouping.
- `GROUP BY` creates groups based on matching values.
- `HAVING` filters groups after grouping.
- `AVG()` calculates averages.
- `COUNT()` counts records.
- `SUM()` calculates totals.
- `AND` requires all conditions to be true.
- `OR` requires at least one condition to be true.
- `WHERE` and `HAVING` can be used in the same query.

## ✅ Day 9 Status

- [x] Learned `HAVING`.
- [x] Understood `WHERE` vs `HAVING`.
- [x] Practised `GROUP BY`.
- [x] Used `AVG()`, `COUNT()`, and `SUM()`.
- [x] Solved all 10 SQL practice tasks.

**Next Goal:** Continue learning SQL step by step and apply these concepts to real-world datasets as part of my Data Analyst journey.

#SQL #DataAnalytics #LearningSQL #Day9 #100DaysOfLearning
