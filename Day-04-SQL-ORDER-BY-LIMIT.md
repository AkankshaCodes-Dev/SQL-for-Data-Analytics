
# Day 04 - SQL ORDER BY and LIMIT

## Topics Covered
- ORDER BY ASC and DESC
- Sorting by multiple columns
- LIMIT clause
- Filtering and finding top results

## 1. Sort Salaries from Highest to Lowest

```sql
SELECT *
FROM Employees
ORDER BY Salary DESC;
```

## 2. Find the Three Lowest-Paid Employees

```sql
SELECT *
FROM Employees
ORDER BY Salary ASC
LIMIT 3;
```

## 3. Sort by Department and Salary

```sql
SELECT *
FROM Employees
ORDER BY Department ASC, Salary DESC;
```

## 4. Find the Highest-Paid Employee in Sales

```sql
SELECT *
FROM Employees
WHERE Department = 'Sales'
ORDER BY Salary DESC
LIMIT 1;
```

## Key Learnings
- ASC sorts in ascending order.
- DESC sorts in descending order.
- Multiple-column sorting applies sorting rules in sequence.
- LIMIT restricts the number of rows returned.
- WHERE filters data before sorting and limiting.

## Status
Day 04 SQL practice completed.
