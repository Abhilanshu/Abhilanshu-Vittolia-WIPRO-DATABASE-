## Question 1

### Problem Statement

Display the ENAME, SAL and COMM of employees who earn commission and sort the records in descending order of salary and commission. Use column's numeric position in the ORDER BY clause.

### SQL Query

```sql
SELECT ENAME, SAL, COMM
FROM EMP
WHERE COMM IS NOT NULL
ORDER BY 2 DESC, 3 DESC;
```

### Explanation

- `WHERE COMM IS NOT NULL` returns employees who receive commission.
- `ORDER BY 2 DESC` sorts by the second selected column (`SAL`) in descending order.
- `ORDER BY 3 DESC` sorts by the third selected column (`COMM`) in descending order if salaries are equal.

### Concept Learned

- IS NULL / IS NOT NULL
- ORDER BY
- Numeric position in ORDER BY

## Question 2

### Problem Statement

The HR department needs a query to display all unique job codes from the `EMP` table.

### SQL Query

```sql
SELECT DISTINCT JOB
FROM EMP;
```

### Explanation

- `DISTINCT` removes duplicate values from the selected column.
- `JOB` specifies the column to retrieve.
- `FROM EMP` specifies the source table.

### Concept Learned

- `DISTINCT` is used to retrieve unique values from a column.
- It eliminates duplicate rows from the query result.

## Question 3

### Problem Statement

The HR department wants more descriptive column headings for its employee report. Rename the column headings as **Emp #**, **Employee**, **Job**, and **Hire Date** using column aliases.

### SQL Query

```sql
SELECT EMPNO AS "Emp #",
       ENAME AS "Employee",
       JOB AS "Job",
       HIREDATE AS "Hire Date"
FROM EMP;
```

### Explanation

- `AS` is used to assign a new name (alias) to a column.
- Double quotes are required when the alias contains spaces or special characters.
- The aliases only affect the output display and do not modify the table structure.

### Concept Learned

- `AS` is used to rename column headings.
- Double quotes are required for aliases containing spaces or special characters.
- Column aliases improve the readability of query results.

## Question 4

### Problem Statement

The HR department has requested a report of all employees and their job IDs. Display the employee name concatenated with the job ID (separated by a comma and a space) and name the column **Employee and Title** using a column alias.

### SQL Query

```sql
SELECT ENAME || ', ' || JOB AS "Employee and Title"
FROM EMP;
```

### Explanation

- `||` is the concatenation operator in Oracle SQL.
- `', '` adds a comma and a space between the employee name and job title.
- `AS "Employee and Title"` assigns a meaningful heading to the output column.

### Concept Learned

- `||` concatenates two or more strings.
- String literals are enclosed in single quotes.
- Column aliases improve the readability of query results.

## Question 5

### Problem Statement

Create a query to display the employee name, job, hire date, and manager ID in a single column. Separate each value with a comma and name the column **THE_OUTPUT**.

### SQL Query

```sql
SELECT ENAME || ', ' || JOB || ', ' || HIREDATE || ', ' || MGR AS THE_OUTPUT
FROM EMP;
```

### Explanation

- `||` concatenates multiple column values into a single string.
- `', '` inserts a comma and a space between each value.
- `AS THE_OUTPUT` assigns the required column heading.

### Concept Learned

- Multiple columns can be concatenated using the `||` operator.
- String literals can be inserted while concatenating.
- Column aliases make the output more readable.

## Question 6

### Problem Statement

Create a report to display the employee name, job, and hire date for employees whose names are **SCOTT** or **TURNER**. Display the results in ascending order of hire date.

### SQL Query

```sql
SELECT ENAME, JOB, HIREDATE
FROM EMP
WHERE ENAME IN ('SCOTT', 'TURNER')
ORDER BY HIREDATE ASC;
```

### Explanation

- `IN` is used to match multiple values in a single condition.
- `ORDER BY HIREDATE ASC` sorts the records in ascending order of hire date.
- `ASC` specifies ascending order (default).

### Concept Learned

- `IN` simplifies multiple equality conditions.
- `ORDER BY` sorts query results.
- `ASC` sorts in ascending order, while `DESC` sorts in descending order.

## Question 7

### Problem Statement

Display the employee name (`ENAME`) and department number (`DEPTNO`) of all employees in departments **20** or **30**. Display the results in ascending alphabetical order by employee name.

### SQL Query

```sql
SELECT ENAME, DEPTNO
FROM EMP
WHERE DEPTNO IN (20, 30)
ORDER BY ENAME ASC;
```

### Explanation

- `IN (20, 30)` filters rows where the department number is either 20 or 30.
- `ORDER BY ENAME ASC` sorts the employees alphabetically by name.
- `ASC` specifies ascending order.

### Concept Learned

- `IN` is used to filter multiple values of the same column.
- `ORDER BY` sorts query results.
- Character columns are sorted alphabetically by default in ascending order.

## Question 8

### Problem Statement

Display the employee name and salary of employees who earn between **2000** and **3000** and belong to department **20** or **30**. Label the columns as **Employee** and **Monthly Salary**.

### SQL Query

```sql
SELECT ENAME AS "Employee",
       SAL AS "Monthly Salary"
FROM EMP
WHERE SAL BETWEEN 2000 AND 3000
  AND DEPTNO IN (20, 30);
```

### Explanation

- `BETWEEN` selects values within a specified range (inclusive).
- `IN` filters employees belonging to departments 20 or 30.
- `AND` combines both conditions.
- `AS` provides meaningful column headings.

### Concept Learned

- `BETWEEN` is used for range-based filtering.
- `BETWEEN` includes both boundary values.
- `AND` requires all conditions to be true.
- `IN` is used to match multiple values of the same column.

## Question 9

### Problem Statement

Display the employee name (`ENAME`) and hire date (`HIREDATE`) for all employees who were hired in **1981**.

### SQL Query

```sql
SELECT ENAME, HIREDATE
FROM EMP
WHERE HIREDATE BETWEEN '01-JAN-1981' AND '31-DEC-1981';
```

### Explanation

- `SELECT ENAME, HIREDATE` retrieves the required columns.
- `FROM EMP` specifies the source table.
- `BETWEEN '01-JAN-1981' AND '31-DEC-1981'` filters employees hired during the year 1981.
- `BETWEEN` includes both the start and end dates.

### Concept Learned

- `BETWEEN` can be used with date values.
- Oracle stores dates using the `DATE` data type.
- Date range filtering is commonly used in SQL queries.

## Question 10

### Problem Statement

Display the employee name (`ENAME`) and salary (`SAL`) of employees who earn more than an amount specified by the user at runtime.

### SQL Query

```sql
SELECT ENAME, SAL
FROM EMP
WHERE SAL > &salary;
```

### Explanation

- `&salary` is a substitution variable in Oracle SQL*Plus.
- The user is prompted to enter a salary value when the query is executed.
- The entered value is substituted into the query before execution.

### Concept Learned

- `&` is used to create substitution variables in Oracle SQL*Plus.
- Substitution variables allow dynamic user input at runtime.
- They make SQL queries reusable without modifying the query text.

## Question 11

### Problem Statement

Create a report to display the employee name (`ENAME`) and job title (`JOB`) of all employees who do not have a manager.

### SQL Query

```sql
SELECT ENAME, JOB
FROM EMP
WHERE MGR IS NULL;
```

### Explanation

- `SELECT ENAME, JOB` retrieves the required columns.
- `FROM EMP` specifies the source table.
- `IS NULL` filters rows where the manager ID is not assigned.

### Concept Learned

- `NULL` represents an unknown or missing value.
- Use `IS NULL` to check for missing values.
- Do **not** use `=` or `!=` with `NULL`.

## Question 12

### Problem Statement

Create a query that prompts the user for a **Manager ID** and displays the employee number (`EMPNO`), employee name (`ENAME`), salary (`SAL`), and department number (`DEPTNO`). Allow the user to choose the column used for sorting the results.

### SQL Query

```sql
SELECT EMPNO, ENAME, SAL, DEPTNO
FROM EMP
WHERE MGR = &manager_id
ORDER BY &sort_column;
```

### Explanation

- `&manager_id` prompts the user to enter a manager ID.
- `WHERE MGR = &manager_id` filters employees reporting to the specified manager.
- `&sort_column` prompts the user to enter the column name used for sorting.
- `ORDER BY` sorts the result based on the selected column.

### Concept Learned

- Substitution variables (`&`) allow dynamic user input.
- `ORDER BY` can use a user-specified column in Oracle SQL*Plus.
- Dynamic queries improve flexibility without modifying the SQL statement.

## Question 13

### Problem Statement

Display the employee name (`ENAME`) and salary (`SAL`) of employees whose names end with the letter **'N'**.

### SQL Query

```sql
SELECT ENAME, SAL
FROM EMP
WHERE ENAME LIKE '%N';
```

### Explanation

- `LIKE` is used to search for a specified pattern in a character column.
- `%` represents zero or more characters.
- `%N` matches names that end with the letter **N**.

### Concept Learned

- `LIKE` is used for pattern matching.
- `%` matches any number of characters.
- `%N` filters values ending with **N**.

## Question 14

### Problem Statement

Display the employee names (`ENAME`) in which the **third letter is 'A'**.

### SQL Query

```sql
SELECT ENAME
FROM EMP
WHERE ENAME LIKE '__A%';
```

### Explanation

- `LIKE` is used for pattern matching.
- Each `_` represents exactly one character.
- `A` specifies that the third character must be the letter **A**.
- `%` matches any remaining characters after the third position.

### Concept Learned

- `_` matches exactly one character.
- `%` matches zero or more characters.
- `LIKE '__A%'` finds names whose third letter is **A**.

## Question 15

### Problem Statement

Display the employee names (`ENAME`) that contain both the letters **A** and **S**.

### SQL Query

```sql
SELECT ENAME
FROM EMP
WHERE ENAME LIKE '%A%S%'
   OR ENAME LIKE '%S%A%';
```

### Explanation

- `%A%S%` matches names where **A** appears before **S**.
- `%S%A%` matches names where **S** appears before **A**.
- `OR` ensures that names containing both letters are returned regardless of their order.

### Concept Learned

- `LIKE` can be combined with `%` to search for multiple characters.
- `OR` can be used to match multiple patterns.
- Pattern matching is useful when the exact position of characters is unknown.

## Question 16

### Problem Statement

Display the employee name (`ENAME`), job (`JOB`), and salary (`SAL`) of all employees whose job is **CLERK** and whose salary is **800**, **950**, or **1300**.

### SQL Query

```sql
SELECT ENAME, JOB, SAL
FROM EMP
WHERE JOB = 'CLERK'
  AND SAL IN (800, 950, 1300);
```

### Explanation

- `JOB = 'CLERK'` filters employees whose job title is **CLERK**.
- `SAL IN (800, 950, 1300)` filters employees whose salary matches one of the specified values.
- `AND` ensures that both conditions are satisfied.

### Concept Learned

- `IN` is used to compare a column with multiple values.
- `AND` combines multiple conditions that must all be true.
- String values are enclosed in single quotes.