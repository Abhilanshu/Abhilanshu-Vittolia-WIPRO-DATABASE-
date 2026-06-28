# Single Row Functions

## Types of Single Row Functions

- Character Functions
  - UPPER()
  - LOWER()
  - INITCAP()
  - LENGTH()
  - SUBSTR()
  - INSTR()

- Number Functions
  - ROUND()
  - TRUNC()
  - MOD()

- Date Functions
  - SYSDATE
  - MONTHS_BETWEEN()
  - ADD_MONTHS()
  - NEXT_DAY()

- Conversion Functions
  - TO_CHAR()
  - TO_DATE()
  - TO_NUMBER()

## Question 1

### Problem Statement

Write a query to display the current system date. Label the column **Date**.

### SQL Query

```sql
SELECT SYSDATE AS "Date"
FROM DUAL;
```

### Explanation

- `SYSDATE` returns the current system date and time.
- `AS "Date"` assigns a user-friendly column heading.
- `DUAL` is Oracle's special one-row dummy table used when no actual table is required.

### Concept Learned

- `SYSDATE` is a built-in Oracle date function.
- `DUAL` is used when selecting expressions or functions without referencing a database table.
- `AS` provides a meaningful alias for the output column.

## Question 2

### Problem Statement

Display the employee number (`EMPNO`), employee name (`ENAME`), current salary (`SAL`), and salary increased by **15.5%**. Display the increased salary as a whole number and label the column **New Salary**.

### SQL Query

```sql
SELECT EMPNO,
       ENAME,
       SAL,
       ROUND(SAL * 1.155) AS "New Salary"
FROM EMP;
```

### Explanation

- `SAL * 1.155` increases the salary by **15.5%**.
- `ROUND()` rounds the calculated salary to the nearest whole number.
- `AS "New Salary"` provides a meaningful heading for the calculated column.

### Concept Learned

- Arithmetic expressions can be used inside a `SELECT` statement.
- `ROUND()` rounds a numeric value to the nearest whole number.
- Calculated columns can be assigned aliases using `AS`.

## Question 3

### Problem Statement

Modify the previous query to display the salary increase by subtracting the old salary from the new salary. Label the new column **Increase**.

### SQL Query

```sql
SELECT EMPNO,
       ENAME,
       SAL,
       ROUND(SAL * 1.155) AS "New Salary",
       ROUND(SAL * 1.155) - SAL AS "Increase"
FROM EMP;
```

### Explanation

- `ROUND(SAL * 1.155)` calculates the salary after a **15.5% increase**.
- `ROUND(SAL * 1.155) - SAL` calculates the amount of salary increase.
- `AS` is used to assign meaningful column names.

### Concept Learned

- Arithmetic operations can be performed using calculated columns.
- `ROUND()` is useful for returning whole-number values.
- Multiple calculated columns can be displayed in a single query.

## Question 4

### Problem Statement

Display the employee name with the first letter in uppercase and the remaining letters in lowercase. Also display the length of the employee name for employees whose names start with **J**, **A**, or **M**. Sort the results alphabetically by employee name.

### SQL Query

```sql
SELECT INITCAP(ENAME) AS "Employee Name",
       LENGTH(ENAME) AS "Name Length"
FROM EMP
WHERE ENAME LIKE 'J%'
   OR ENAME LIKE 'A%'
   OR ENAME LIKE 'M%'
ORDER BY ENAME;
```

### Explanation

- `INITCAP(ENAME)` converts the first letter to uppercase and the remaining letters to lowercase.
- `LENGTH(ENAME)` returns the number of characters in the employee name.
- `LIKE 'J%'`, `LIKE 'A%'`, and `LIKE 'M%'` filter employee names starting with J, A, or M.
- `ORDER BY ENAME` sorts the results alphabetically.

### Concept Learned

- `INITCAP()` formats text by capitalizing the first letter.
- `LENGTH()` returns the number of characters in a string.
- `LIKE` is used for pattern matching.
- `ORDER BY` sorts the query result.

## Question 5

### Problem Statement

Rewrite the previous query so that the user is prompted to enter a starting letter. Display the employee name with proper capitalization and the length of the employee name for employees whose names start with the entered letter.

### SQL Query

```sql
SELECT INITCAP(ENAME) AS "Employee Name",
       LENGTH(ENAME) AS "Name Length"
FROM EMP
WHERE ENAME LIKE '&letter%'
ORDER BY ENAME;
```

### Explanation

- `INITCAP(ENAME)` formats the employee name.
- `LENGTH(ENAME)` returns the number of characters in the name.
- `&letter` prompts the user to enter a starting letter.
- `LIKE '&letter%'` matches employee names beginning with the entered letter.
- `ORDER BY ENAME` sorts the results alphabetically.

### Concept Learned

- Substitution variables allow dynamic user input.
- `LIKE` performs pattern matching.
- `%` matches zero or more characters.
- String functions can be combined with filtering conditions.

## Question 6

### Problem Statement

Display the employee name and the number of months the employee has worked from the hire date until today. Round the result to the nearest whole number, label the column **MONTHS_WORKED**, and display the results in ascending order of months worked.

### SQL Query

```sql
SELECT ENAME,
       ROUND(MONTHS_BETWEEN(SYSDATE, HIREDATE)) AS MONTHS_WORKED
FROM EMP
ORDER BY MONTHS_WORKED;
```

### Explanation

- `MONTHS_BETWEEN(SYSDATE, HIREDATE)` calculates the number of months between today and the employee's hire date.
- `ROUND()` rounds the calculated months to the nearest whole number.
- `AS MONTHS_WORKED` assigns a meaningful column heading.
- `ORDER BY MONTHS_WORKED` sorts the results by the number of months worked.

### Concept Learned

- `MONTHS_BETWEEN()` calculates the difference between two dates in months.
- `SYSDATE` returns the current system date.
- `ROUND()` rounds numeric values.
- `ORDER BY` sorts the output.

## Question 7

### Problem Statement

Create a report that displays each employee's name followed by the message **"earns monthly but wants"** and three times their salary. Label the column **Dream Salaries**.

### SQL Query

```sql
SELECT ENAME || ' earns monthly but wants ' || (SAL * 3) AS "Dream Salaries"
FROM EMP;
```

### Explanation

- `ENAME` retrieves the employee name.
- `' earns monthly but wants '` is a string literal.
- `SAL * 3` calculates three times the employee's salary.
- `||` concatenates strings and values into a single output.
- `AS "Dream Salaries"` assigns the required column heading.

### Concept Learned

- `||` is used to concatenate strings in Oracle.
- Arithmetic expressions can be combined with string values.
- Oracle automatically converts numeric values to strings during concatenation.

## Question 8

### Problem Statement

Display the employee name (`ENAME`) and salary (`SAL`) for all employees. Format the salary so that it is **15 characters wide**, left-padded with the `$` symbol. Label the salary column **SALARY**.

### SQL Query

```sql
SELECT ENAME,
       LPAD(TO_CHAR(SAL), 15, '$') AS SALARY
FROM EMP;
```

### Explanation

- `TO_CHAR(SAL)` converts the numeric salary into a character string.
- `LPAD(..., 15, '$')` pads the salary with `$` symbols on the left until the total length is 15 characters.
- `AS SALARY` assigns the required column heading.

### Concept Learned

- `TO_CHAR()` converts numbers to character strings.
- `LPAD()` pads a string on the left with a specified character.
- Formatting functions improve the readability of query output.

## Question 9

### Problem Statement

Display each employee's name, hire date, and salary review date. The review date should be the **first Monday after six months of service**. Label the review date column **REVIEW** and format it as:

`Monday, the Thirty-First of July, 2000`

### SQL Query

```sql
SELECT ENAME,
       HIREDATE,
       TO_CHAR(
           NEXT_DAY(ADD_MONTHS(HIREDATE, 6), 'MONDAY'),
           'Day, "the" DDSPTH "of" Month, YYYY'
       ) AS REVIEW
FROM EMP;
```

### Explanation

- `ADD_MONTHS(HIREDATE, 6)` adds six months to the hire date.
- `NEXT_DAY(..., 'MONDAY')` returns the first Monday after that date.
- `TO_CHAR()` formats the review date in a readable format.
- `AS REVIEW` assigns the required column heading.

### Concept Learned

- `ADD_MONTHS()` adds a specified number of months to a date.
- `NEXT_DAY()` returns the next specified weekday.
- `TO_CHAR()` formats dates according to a format model.

## Question 10

### Problem Statement

Display the employee name (`ENAME`), hire date (`HIREDATE`), and the day of the week on which the employee was hired. Label the day column **DAY** and display the results starting with Monday.

### SQL Query

```sql
SELECT ENAME,
       HIREDATE,
       TO_CHAR(HIREDATE, 'FMDay') AS DAY
FROM EMP
ORDER BY CASE TO_CHAR(HIREDATE, 'FMDay')
           WHEN 'Monday' THEN 1
           WHEN 'Tuesday' THEN 2
           WHEN 'Wednesday' THEN 3
           WHEN 'Thursday' THEN 4
           WHEN 'Friday' THEN 5
           WHEN 'Saturday' THEN 6
           WHEN 'Sunday' THEN 7
         END;
```

### Explanation

- `TO_CHAR(HIREDATE, 'FMDay')` extracts the weekday name without trailing spaces.
- `AS DAY` assigns the required column heading.
- The `CASE` expression assigns an order to each weekday so the output starts with Monday instead of alphabetical order.

### Concept Learned

- `TO_CHAR()` extracts and formats parts of a date.
- `FM` removes extra spaces from formatted output.
- `CASE` can be used to implement custom sorting logic.

## Question 11

### Problem Statement

Display the employee name (`ENAME`) and commission (`COMM`). If an employee does not earn a commission, display **No Commission** instead. Label the column **COMM**.

### SQL Query

```sql
SELECT ENAME,
       NVL(TO_CHAR(COMM), 'No Commission') AS COMM
FROM EMP;
```

### Explanation

- `TO_CHAR(COMM)` converts the numeric commission into a character string.
- `NVL()` replaces `NULL` commission values with the text **No Commission**.
- `AS COMM` assigns the required column heading.

### Concept Learned

- `NVL()` replaces `NULL` values with a specified replacement.
- `TO_CHAR()` is used when replacing numeric values with text.
- `NULL` values can be displayed in a user-friendly format.

## Question 12

### Problem Statement

Display the first eight characters of each employee's name and represent the salary using asterisks (`*`), where each asterisk represents $1000. Sort the results in descending order of salary.

### SQL Query

```sql
SELECT SUBSTR(ENAME, 1, 8) AS EMPLOYEE,
       RPAD('*', TRUNC(SAL / 1000), '*') AS SALARY
FROM EMP
ORDER BY SAL DESC;
```

### Explanation

- `SUBSTR(ENAME, 1, 8)` returns the first eight characters of the employee name.
- `TRUNC(SAL / 1000)` calculates the number of thousands in the salary.
- `RPAD('*', TRUNC(SAL / 1000), '*')` creates a salary chart using asterisks.
- `ORDER BY SAL DESC` sorts employees from highest to lowest salary.

### Concept Learned

- `SUBSTR()` extracts part of a string.
- `TRUNC()` removes the decimal part of a number.
- `RPAD()` pads a string on the right and can be used to create simple text-based charts.

## Question 13

### Problem Statement

Using the `DECODE()` function, display the grade of all employees based on their job.

- PRESIDENT → A
- MANAGER → B
- SALESMAN → C
- CLERK → D

### SQL Query

```sql
SELECT ENAME,
       JOB,
       DECODE(JOB,
              'PRESIDENT', 'A',
              'MANAGER', 'B',
              'SALESMAN', 'C',
              'CLERK', 'D',
              'Not Assigned') AS GRADE
FROM EMP;
```

### Explanation

- `DECODE()` compares the value of `JOB`.
- If the job matches one of the specified values, it returns the corresponding grade.
- The last argument (`'Not Assigned'`) acts as the default value if no match is found.

### Concept Learned

- `DECODE()` performs conditional comparisons.
- It is Oracle-specific and works similarly to an `IF-ELSE` statement.

## Question 14

### Problem Statement

Rewrite the previous query using the `CASE` expression.

### SQL Query

```sql
SELECT ENAME,
       JOB,
       CASE
           WHEN JOB = 'PRESIDENT' THEN 'A'
           WHEN JOB = 'MANAGER' THEN 'B'
           WHEN JOB = 'SALESMAN' THEN 'C'
           WHEN JOB = 'CLERK' THEN 'D'
           ELSE 'Not Assigned'
       END AS GRADE
FROM EMP;
```

### Explanation

- `CASE` evaluates conditions one by one.
- When a condition is true, it returns the corresponding result.
- `ELSE` provides the default value if no condition matches.

### Concept Learned

- `CASE` is the SQL standard conditional expression.
- It is more flexible and portable than `DECODE()`.