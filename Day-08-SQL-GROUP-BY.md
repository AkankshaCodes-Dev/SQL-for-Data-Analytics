# Day 8 — SQL GROUP BY | Personal Data Analytics Practice

## 📌 Overview

On Day 8 of my personal Data Analytics learning journey, I learned how to use SQL `GROUP BY` with aggregate functions to summarize data and generate department-wise and city-wise insights.

## 🎯 Learning Objectives

- Understand the `GROUP BY` clause.
- Use aggregate functions: `COUNT()`, `SUM()`, `AVG()`, `MAX()`, and `MIN()`.
- Group data by one or multiple columns.
- Understand the difference between `WHERE` and `HAVING`.
- Sort aggregated results using `ORDER BY`.
- Practice SQL queries using an employee dataset.

## 📚 Concepts Learned

| Concept | Purpose |
|---|---|
| `GROUP BY` | Groups rows with matching values |
| `COUNT()` | Counts rows or non-NULL values |
| `SUM()` | Calculates a total |
| `AVG()` | Calculates an average |
| `MAX()` | Finds the maximum value |
| `MIN()` | Finds the minimum value |
| `WHERE` | Filters rows before grouping |
| `HAVING` | Filters groups after aggregation |
| `ORDER BY` | Sorts query results |
| Multiple-column grouping | Groups data by combinations of columns |

## 🗃️ Practice Dataset

**Table name:** `Employees`

| EmployeeID | EmployeeName | Department | City | Salary |
|---:|---|---|---|---:|
| 1 | Anu | HR | Bangalore | 20000 |
| 2 | Ravi | IT | Chennai | 30000 |
| 3 | Priya | HR | Bangalore | 25000 |
| 4 | Kiran | IT | Mumbai | 35000 |
| 5 | Meena | Sales | Chennai | 22000 |
| 6 | Arjun | Sales | Bangalore | 28000 |
| 7 | Sneha | IT | Chennai | 40000 |
| 8 | Rahul | HR | Mumbai | 30000 |
| 9 | Divya | Sales | Mumbai | 32000 |
| 10 | Neha | IT | Bangalore | 25000 |

## 💻 SQL Examples

### 1. Count employees in each department

```sql
SELECT Department, COUNT(*) AS Total_Employees
FROM Employees
GROUP BY Department;
```

### 2. Calculate total salary by department

```sql
SELECT Department, SUM(Salary) AS Total_Salary
FROM Employees
GROUP BY Department;
```

### 3. Calculate average salary by department

```sql
SELECT Department, AVG(Salary) AS Average_Salary
FROM Employees
GROUP BY Department;
```

### 4. Find the highest and lowest salaries

```sql
SELECT
    Department,
    MAX(Salary) AS Highest_Salary,
    MIN(Salary) AS Lowest_Salary
FROM Employees
GROUP BY Department;
```

### 5. Group by department and city

```sql
SELECT Department, City, COUNT(*) AS Total_Employees
FROM Employees
GROUP BY Department, City;
```

### 6. Filter groups using HAVING

```sql
SELECT Department, SUM(Salary) AS Total_Salary
FROM Employees
GROUP BY Department
HAVING SUM(Salary) > 80000;
```

### 7. Sort departments by total salary

```sql
SELECT Department, SUM(Salary) AS Total_Salary
FROM Employees
GROUP BY Department
ORDER BY Total_Salary DESC;
```

## 📝 Practice Questions — 15 Tasks

1. Display the total number of employees in the company.
2. Count employees in each department.
3. Calculate the total salary paid by each department.
4. Calculate the average salary for each department.
5. Find the highest salary in each department.
6. Find the lowest salary in each department.
7. Count employees in each city.
8. Calculate the total salary for each city.
9. Calculate the average salary for each city.
10. Count employees for each department-city combination.
11. Calculate total salary for each department-city combination.
12. Count employees in each department whose salary is at least ₹30,000.
13. Display departments whose total salary is greater than ₹80,000.
14. Display departments whose average salary is greater than ₹30,000.
15. Display departments in descending order of total salary.

## 💡 Key Takeaways

- `GROUP BY` helps summarize data by categories.
- Aggregate functions make it easier to analyze totals, averages, counts, minimums, and maximums.
- Multiple-column grouping provides more detailed insights.
- `WHERE` filters individual rows, while `HAVING` filters grouped results.
- `ORDER BY` helps arrange the final output.

## 🚀 Learning Outcome

I practiced SQL aggregation and grouping using employee data. These concepts are useful for analyzing sales, salaries, customer data, and business performance.

**Day 8 Status:** SQL learning and practice completed.

#SQL #DataAnalytics #SQLPractice #LearningJourney
