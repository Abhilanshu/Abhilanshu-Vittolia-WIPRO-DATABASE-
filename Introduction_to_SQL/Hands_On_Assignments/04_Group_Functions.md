## Question 1

### Problem Statement

Display the highest salary, lowest salary, total salary, and average salary of all employees. Label the columns appropriately.

### SQL Query

```sql
SELECT MAX(SAL) AS HIGHEST_SALARY,
       MIN(SAL) AS LOWEST_SALARY,
       SUM(SAL) AS TOTAL_SALARY,
       AVG(SAL) AS AVERAGE_SALARY
FROM EMP;
```

### Explanation

- `MAX(SAL)` returns the highest salary.
- `MIN(SAL)` returns the lowest salary.
- `SUM(SAL)` returns the total of all salaries.
- `AVG(SAL)` returns the average salary.
- `AS` assigns meaningful column names.

### Concept Learned

- Aggregate functions perform calculations on multiple rows and return a single result.

## Question 2

### Problem Statement

Display the maximum salary, minimum salary, total salary, and average salary of all employees. Round all values to the nearest whole number.

### SQL Query

```sql
SELECT ROUND(MAX(SAL)) AS MAXIMUM,
       ROUND(MIN(SAL)) AS MINIMUM,
       ROUND(SUM(SAL)) AS SUM,
       ROUND(AVG(SAL)) AS AVERAGE
FROM EMP;
```

### Explanation

- `MAX(SAL)` returns the highest salary.
- `MIN(SAL)` returns the lowest salary.
- `SUM(SAL)` calculates the total salary.
- `AVG(SAL)` calculates the average salary.
- `ROUND()` rounds each value to the nearest whole number.

### Concept Learned

- Aggregate functions can be combined with other functions.
- `ROUND()` is commonly used with `AVG()` to improve readability.

## Question 3

### Problem Statement

Display the minimum, maximum, total, and average salary for each job type.

### SQL Query

```sql
SELECT JOB,
       MIN(SAL) AS MINIMUM,
       MAX(SAL) AS MAXIMUM,
       SUM(SAL) AS TOTAL_SALARY,
       ROUND(AVG(SAL)) AS AVERAGE_SALARY
FROM EMP
GROUP BY JOB;
```

### Explanation

- `GROUP BY JOB` groups employees based on their job.
- `MIN(SAL)` returns the lowest salary for each job.
- `MAX(SAL)` returns the highest salary for each job.
- `SUM(SAL)` returns the total salary for each job.
- `AVG(SAL)` returns the average salary for each job.
- `ROUND()` rounds the average salary to the nearest whole number.

### Concept Learned

- `GROUP BY` divides rows into groups based on one or more columns.
- Aggregate functions are calculated separately for each group.

## Question 4

### Problem Statement

Display the number of employees having the same job.

### SQL Query

```sql
SELECT JOB,
       COUNT(*) AS NUMBER_OF_EMPLOYEES
FROM EMP
GROUP BY JOB;
```

### Explanation

- `COUNT(*)` counts the number of employees.
- `GROUP BY JOB` groups employees according to their job.
- `AS NUMBER_OF_EMPLOYEES` assigns a meaningful column heading.

### Concept Learned

- `COUNT()` counts the number of rows.
- `GROUP BY` is used to count rows within each group.

## Question 5

### Problem Statement

Determine the number of managers without listing them. Label the column **Number of Managers**.

### SQL Query

```sql
SELECT COUNT(*) AS "Number of Managers"
FROM EMP
WHERE JOB = 'MANAGER';
```

### Explanation

- `WHERE JOB = 'MANAGER'` filters only the manager records.
- `COUNT(*)` counts the filtered rows.
- `AS "Number of Managers"` provides the required column heading.

### Concept Learned

- `WHERE` filters rows before aggregate functions are applied.
- `COUNT(*)` counts the number of matching rows.

## Question 6

### Problem Statement

Display the difference between the highest salary and the lowest salary. Label the column **DIFFERENCE**.

### SQL Query

```sql
SELECT MAX(SAL) - MIN(SAL) AS DIFFERENCE
FROM EMP;
```

### Explanation

- `MAX(SAL)` returns the highest salary.
- `MIN(SAL)` returns the lowest salary.
- `MAX(SAL) - MIN(SAL)` calculates the difference between them.
- `AS DIFFERENCE` assigns the required column heading.

### Concept Learned

- Aggregate functions can be used inside arithmetic expressions.
- SQL allows calculations using the results of aggregate functions.

## Question 7

### Problem Statement

Determine the number of managers in each department.

### SQL Query

```sql
SELECT DEPTNO,
       COUNT(*) AS NUMBER_OF_MANAGERS
FROM EMP
WHERE JOB = 'MANAGER'
GROUP BY DEPTNO;
```

### Explanation

- `WHERE JOB = 'MANAGER'` filters only manager records.
- `GROUP BY DEPTNO` groups managers by department.
- `COUNT(*)` counts the number of managers in each department.
- `AS NUMBER_OF_MANAGERS` provides a meaningful column heading.

### Concept Learned

- `WHERE` filters rows before grouping.
- `GROUP BY` creates department-wise groups.
- `COUNT()` returns the number of rows in each group.

## Question 8

### Problem Statement

Determine the number of distinct managers.

### SQL Query

```sql
SELECT COUNT(DISTINCT MGR) AS NUMBER_OF_MANAGERS
FROM EMP;
```

### Explanation

- `DISTINCT` removes duplicate manager IDs.
- `COUNT(DISTINCT MGR)` counts the number of unique managers.
- `COUNT(column)` ignores `NULL` values.
- `AS NUMBER_OF_MANAGERS` provides a meaningful column heading.

### Concept Learned

- `DISTINCT` returns only unique values.
- `COUNT(DISTINCT column)` counts unique non-NULL values.