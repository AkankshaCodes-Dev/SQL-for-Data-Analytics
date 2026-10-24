# Day 11 — SQL: Conditional Business Analysis

## 📌 Overview
On Day 11 of my SQL for Data Analytics learning journey, I practised combining `WHERE`, `CASE WHEN`, `GROUP BY`, and `HAVING` to solve business-style data analysis problems.

I focused on filtering employee records, creating salary categories, aggregating data, and identifying departments that meet specific business conditions.

## 🎯 Learning Objectives
- Combine SQL filtering and aggregation techniques.
- Use `CASE WHEN` to create conditional categories.
- Understand the difference between `WHERE` and `HAVING`.
- Group records by department and region.
- Answer business questions using a single dataset.

## 🗂️ Practice Dataset: Employees

| EmployeeID | Name | Department | Region | Salary |
|---:|---|---|---|---:|
| 1 | Ravi | IT | South | 50000 |
| 2 | Priya | HR | North | 35000 |
| 3 | Amit | IT | South | 60000 |
| 4 | Sneha | Sales | North | 40000 |
| 5 | Kiran | Sales | South | 45000 |
| 6 | Neha | HR | South | 30000 |
| 7 | Arjun | IT | North | 55000 |
| 8 | Divya | Sales | North | 50000 |
| 9 | Rahul | HR | North | 40000 |
| 10 | Meena | IT | South | 45000 |

## 📚 Concepts Learned

### 1. WHERE — Filtering Rows
`WHERE` filters individual records before grouping.

```sql
SELECT *
FROM Employees
WHERE Salary > 45000;
```

Use case: Find employees earning more than ₹45,000.

### 2. CASE WHEN — Conditional Categories
`CASE WHEN` assigns categories based on conditions.

```sql
SELECT Name, Salary,
       CASE
           WHEN Salary >= 50000 THEN 'High'
           WHEN Salary >= 40000 THEN 'Medium'
           ELSE 'Low'
       END AS Salary_Category
FROM Employees;
```

Classification:
- High: Salary >= ₹50,000
- Medium: Salary >= ₹40,000 and < ₹50,000
- Low: Salary < ₹40,000

### 3. GROUP BY — Aggregation
`GROUP BY` groups records with common values.

```sql
SELECT Department,
       AVG(Salary) AS Average_Salary
FROM Employees
GROUP BY Department;
```

Expected results:

| Department | Average Salary |
|---|---:|
| HR | 35000 |
| IT | 52500 |
| Sales | 45000 |

### 4. HAVING — Filtering Groups
`HAVING` filters aggregated groups after grouping.

```sql
SELECT Department,
       AVG(Salary) AS Average_Salary
FROM Employees
GROUP BY Department
HAVING AVG(Salary) > 40000;
```

Expected results:

| Department | Average Salary |
|---|---:|
| IT | 52500 |
| Sales | 45000 |

### 5. Combining WHERE, CASE WHEN, GROUP BY and HAVING

```sql
SELECT Department,
       AVG(Salary) AS Average_Salary,
       CASE
           WHEN AVG(Salary) >= 50000 THEN 'High'
           ELSE 'Medium'
       END AS Salary_Level
FROM Employees
WHERE Region = 'South'
GROUP BY Department
HAVING AVG(Salary) > 40000;
```

Expected results:

| Department | Average Salary | Salary Level |
|---|---:|---|
| IT | 51666.67 | High |
| Sales | 45000 | Medium |

**Logical processing order:** `FROM → WHERE → GROUP BY → HAVING → SELECT`

## 💻 Practice: 10 Business Questions with Solutions

### Task 1: Find IT employees earning more than ₹45,000.

```sql
SELECT *
FROM Employees
WHERE Department = 'IT'
  AND Salary > 45000;
```

Expected employees: Ravi, Amit and Arjun.

### Task 2: Classify employees by salary.

```sql
SELECT Name, Salary,
       CASE
           WHEN Salary >= 50000 THEN 'High'
           WHEN Salary >= 40000 THEN 'Medium'
           ELSE 'Low'
       END AS Salary_Category
FROM Employees;
```

Expected classification:

| Name | Salary | Category |
|---|---:|---|
| Ravi | 50000 | High |
| Priya | 35000 | Low |
| Amit | 60000 | High |
| Sneha | 40000 | Medium |
| Kiran | 45000 | Medium |
| Neha | 30000 | Low |
| Arjun | 55000 | High |
| Divya | 50000 | High |
| Rahul | 40000 | Medium |
| Meena | 45000 | Medium |

### Task 3: Count employees in each department.

```sql
SELECT Department,
       COUNT(*) AS Employee_Count
FROM Employees
GROUP BY Department;
```

Expected results: HR = 3, IT = 4, Sales = 3.

### Task 4: Calculate average salary by region.

```sql
SELECT Region,
       AVG(Salary) AS Average_Salary
FROM Employees
GROUP BY Region;
```

Expected results:

| Region | Average Salary |
|---|---:|
| North | 44000 |
| South | 46000 |

### Task 5: Find departments with average salary above ₹40,000.

```sql
SELECT Department,
       AVG(Salary) AS Average_Salary
FROM Employees
GROUP BY Department
HAVING AVG(Salary) > 40000;
```

Expected results: IT = ₹52,500; Sales = ₹45,000.

### Task 6: Calculate total salary by department in the South region.

```sql
SELECT Department,
       SUM(Salary) AS Total_Salary
FROM Employees
WHERE Region = 'South'
GROUP BY Department;
```

Expected results:

| Department | Total Salary |
|---|---:|
| HR | 30000 |
| IT | 155000 |
| Sales | 45000 |

### Task 7: Find North-region departments with at least two employees.

```sql
SELECT Department,
       COUNT(*) AS Employee_Count
FROM Employees
WHERE Region = 'North'
GROUP BY Department
HAVING COUNT(*) >= 2;
```

Expected results: HR = 2; Sales = 2.

### Task 8: Calculate average salary by department for employees earning at least ₹40,000.

```sql
SELECT Department,
       AVG(Salary) AS Average_Salary
FROM Employees
WHERE Salary >= 40000
GROUP BY Department;
```

Expected results:

| Department | Average Salary |
|---|---:|
| HR | 40000 |
| IT | 52500 |
| Sales | 45000 |

### Task 9: Count employees in High and Other salary categories.

```sql
SELECT
    CASE
        WHEN Salary >= 50000 THEN 'High'
        ELSE 'Other'
    END AS Salary_Category,
    COUNT(*) AS Employee_Count
FROM Employees
GROUP BY
    CASE
        WHEN Salary >= 50000 THEN 'High'
        ELSE 'Other'
    END;
```

Expected results: High = 4; Other = 6.

### Task 10: Find South-region departments with average salary above ₹40,000 and classify them.

```sql
SELECT Department,
       AVG(Salary) AS Average_Salary,
       CASE
           WHEN AVG(Salary) >= 50000 THEN 'High'
           ELSE 'Medium'
       END AS Salary_Level
FROM Employees
WHERE Region = 'South'
GROUP BY Department
HAVING AVG(Salary) > 40000;
```

Expected results:

| Department | Average Salary | Salary Level |
|---|---:|---|
| IT | 51666.67 | High |
| Sales | 45000 | Medium |

## 🔑 Key Takeaways
- `WHERE` filters individual records.
- `CASE WHEN` creates categories based on conditions.
- `GROUP BY` summarizes data.
- `HAVING` filters aggregated groups.
- Combining these concepts helps answer practical business questions.

## 🚀 Progress
- [x] SQL concepts studied
- [x] Business-style practice questions documented
- [x] Solutions and expected results included

**Day 11 completed — SQL for Data Analytics.**
