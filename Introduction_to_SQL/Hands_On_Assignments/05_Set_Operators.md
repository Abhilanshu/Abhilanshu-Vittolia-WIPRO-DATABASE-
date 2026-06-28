## Question 1

### Problem Statement

Create a matrix report displaying the job, salary for departments 10, 20, and 30, and the total salary for each job.

### SQL Query

```sql
SELECT JOB,
       SUM(DECODE(DEPTNO, 10, SAL, 0)) AS DEPT10,
       SUM(DECODE(DEPTNO, 20, SAL, 0)) AS DEPT20,
       SUM(DECODE(DEPTNO, 30, SAL, 0)) AS DEPT30,
       SUM(SAL) AS TOTAL
FROM EMP
GROUP BY JOB;
```

### Explanation

- `DECODE()` checks the department number and returns the salary only for the matching department.
- `SUM()` adds the salaries for each department.
- `GROUP BY JOB` creates one row for each job.
- `SUM(SAL)` calculates the total salary for each job.

### Concept Learned

- `DECODE()` can be combined with aggregate functions to create matrix (pivot-style) reports.
- `GROUP BY` groups employees based on their job.

## Question 2

### Problem Statement

Using the `UNION` set operator, display the total salary for each department, the total salary for each job, and the overall total salary.

### SQL Query

```sql
SELECT TO_CHAR(DEPTNO) AS TYPE,
       SUM(SAL) AS TOTAL_SALARY
FROM EMP
GROUP BY DEPTNO

UNION

SELECT JOB AS TYPE,
       SUM(SAL) AS TOTAL_SALARY
FROM EMP
GROUP BY JOB

UNION

SELECT 'TOTAL' AS TYPE,
       SUM(SAL) AS TOTAL_SALARY
FROM EMP;
```

### Explanation

- The first query calculates the total salary department-wise.
- The second query calculates the total salary job-wise.
- The third query calculates the grand total salary.
- `TO_CHAR()` converts department numbers into text so that all `SELECT` statements have compatible column types.
- `UNION` combines the results into a single output.

### Concept Learned

- `UNION` combines multiple `SELECT` statements into one result set.
- All queries used with `UNION` must return the same number of columns with compatible data types.

## Question 3

### Problem Statement

Using the `UNION` set operator, display the job and department number of employees working in departments 20, 10, and 30, in that order.

### SQL Query

```sql
SELECT JOB, DEPTNO
FROM EMP
WHERE DEPTNO = 20

UNION

SELECT JOB, DEPTNO
FROM EMP
WHERE DEPTNO = 10

UNION

SELECT JOB, DEPTNO
FROM EMP
WHERE DEPTNO = 30;
```

### Explanation

- The first query retrieves employees from department 20.
- The second query retrieves employees from department 10.
- The third query retrieves employees from department 30.
- `UNION` combines all three result sets into one.

### Concept Learned

- `UNION` combines the output of multiple `SELECT` statements.
- Each `SELECT` statement must have the same number of columns with compatible data types.