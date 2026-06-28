# Retrieving Data Using the SQL SELECT Statement

## Objective

Learn how to retrieve table structure, display table contents, and fetch specific columns using the `SELECT` statement.

---

## Question 1

### Problem Statement

Determine the structure of the `DEPT` table and its contents.

### SQL Query

```sql
DESC DEPT;

SELECT * FROM DEPT;
```

### Explanation

- `DESC DEPT;` displays the table structure, including column names, data types, and constraints.
- `SELECT * FROM DEPT;` retrieves all rows and all columns from the `DEPT` table.

---

## Question 2

### Problem Statement

Determine the structure of the `EMP` table and its contents.

### SQL Query

```sql
DESC EMP;

SELECT * FROM EMP;
```

### Explanation

- `DESC EMP;` displays the structure of the `EMP` table.
- `SELECT * FROM EMP;` displays all employee records.

---

## Question 3

### Problem Statement

Display the employee name (`ENAME`) and department number (`DEPTNO`) of the employee whose employee number (`EMPNO`) is **7788**.

### SQL Query

```sql
SELECT ENAME, DEPTNO
FROM EMP
WHERE EMPNO = 7788;
```

### Explanation

- `SELECT ENAME, DEPTNO` retrieves only the required columns.
- `FROM EMP` specifies the table.
- `WHERE EMPNO = 7788` filters the record for employee number **7788**.

---

## Concepts Learned

- `DESC` command displays the structure of a table.
- `SELECT *` retrieves all columns.
- `SELECT column_name` retrieves specific columns.
- `WHERE` clause filters records based on a condition.