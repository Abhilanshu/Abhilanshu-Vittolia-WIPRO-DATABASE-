# SQL Joins Lab — All 13 Questions

---

# Q1. Natural Join — Addresses of All Departments

**Problem Statement**

The HR department needs a report to display the addresses of all departments. Show the EMPNO, ENAME, SAL, DNAME, and LOC in the output using a NATURAL JOIN.

**SQL Query**

```sql
SELECT E.EMPNO, E.ENAME, E.SAL, D.DNAME, D.LOC
FROM EMP E
NATURAL JOIN DEPT D;
```

**Explanation**

- `NATURAL JOIN` automatically joins EMP and DEPT on the common column `DEPTNO`.
- Oracle detects the matching column name automatically and performs an inner join on it.
- `EMPNO`, `ENAME`, `SAL` come from EMP; `DNAME` and `LOC` come from DEPT.
- Only employees with a matching department are returned (inner join behavior).

**Concept Learned**

- `NATURAL JOIN` joins two tables on all columns with the same name and compatible data types.
- Duplicate join columns are removed from the output automatically.
- Avoid `NATURAL JOIN` if tables share multiple common columns you don't intend to join on.

---

# Q2. Equi Join — SALESMAN Details

**Problem Statement**

The HR department needs a report of all employees. Write a query to display the JOB, MGR, SAL, COMM, and DNAME of employees whose JOB is SALESMAN.

**SQL Query**

```sql
SELECT E.JOB, E.MGR, E.SAL, E.COMM, D.DNAME
FROM EMP E, DEPT D
WHERE E.DEPTNO = D.DEPTNO
AND E.JOB = 'SALESMAN';
```

**Explanation**

- `E.DEPTNO = D.DEPTNO` in the WHERE clause performs an Equi Join between EMP and DEPT.
- `E.JOB = 'SALESMAN'` filters the result to show only salesmen.
- `JOB`, `MGR`, `SAL`, `COMM` are fetched from EMP; `DNAME` is fetched from DEPT.
- Table aliases `E` and `D` are used to avoid ambiguity between columns of the two tables.

**Concept Learned**

- An Equi Join uses the equality operator `=` in the WHERE clause to match related rows from two tables.
- It is the most commonly used join type in SQL.
- Multiple conditions can be combined with `AND` in the WHERE clause to further filter results.

---

# Q3. Equi Join — Employees in DALLAS

**Problem Statement**

The HR department needs a report of employees in LOC DALLAS. Display the ENAME, JOB, DEPTNO, and DNAME for all employees who work in DALLAS.

**SQL Query**

```sql
SELECT E.ENAME, E.JOB, E.DEPTNO, D.DNAME
FROM EMP E, DEPT D
WHERE E.DEPTNO = D.DEPTNO
AND D.LOC = 'DALLAS';
```

**Explanation**

- `E.DEPTNO = D.DEPTNO` connects EMP and DEPT rows using an Equi Join on the department number.
- `D.LOC = 'DALLAS'` filters the output to show only employees working in Dallas.
- `ENAME`, `JOB`, `DEPTNO` come from EMP; `DNAME` comes from DEPT.
- `DEPTNO` is prefixed with `E.` to clearly indicate it is from the EMP table.

**Concept Learned**

- Equi Join can be combined with additional WHERE conditions to filter rows by any column from either table.
- Columns from both tables can be freely selected after a successful join.
- Table aliases make queries shorter and more readable when multiple tables are involved.

---

# Q4. Self Join — Employee and Manager Names

**Problem Statement**

Create a report to display employees ENAME and EMPNO along with their manager's name and manager number. Label the columns Employee, Emp#, Manager, and Mgr#, respectively.

**SQL Query**

```sql
SELECT E.ENAME AS "Employee", E.EMPNO AS "Emp#",
       M.ENAME AS "Manager",  M.EMPNO AS "Mgr#"
FROM EMP E, EMP M
WHERE E.MGR = M.EMPNO;
```

**Explanation**

- The EMP table is joined to itself using two aliases: `E` for employees and `M` for managers.
- `E.MGR = M.EMPNO` links each employee's manager number to the manager's own employee number.
- `E.ENAME`, `E.EMPNO` display employee details; `M.ENAME`, `M.EMPNO` display manager details.
- Column aliases in double quotes like `"Employee"` and `"Emp#"` preserve capitalization and special characters.
- KING has no manager (MGR is NULL), so KING is excluded from this inner join result.

**Concept Learned**

- A Self Join joins a table to itself using two different aliases to distinguish roles like employee vs manager.
- It is used when a table has a column referencing another row in the same table, e.g., MGR references EMPNO.
- Meaningful aliases like `E` and `M` improve query readability in hierarchical data.

---

# Q5. Outer Join — Including KING (No Manager)

**Problem Statement**

Modify the previous query to display all employees including KING, who has no manager. Order the results by the employee number.

**SQL Query**

```sql
SELECT E.ENAME AS "Employee", E.EMPNO AS "Emp#",
       M.ENAME AS "Manager",  M.EMPNO AS "Mgr#"
FROM EMP E, EMP M
WHERE E.MGR = M.EMPNO(+)
ORDER BY E.EMPNO;
```

**Explanation**

- The `(+)` operator on `M.EMPNO` performs a LEFT OUTER JOIN, keeping all rows from EMP E even when there is no matching manager.
- KING, who has NULL in the MGR column, now appears in the result with NULL values for Manager and Mgr#.
- `ORDER BY E.EMPNO` sorts the final output in ascending order of employee number.
- `(+)` is Oracle's traditional outer join syntax; the ANSI equivalent is `LEFT OUTER JOIN`.

**Concept Learned**

- An Outer Join returns all rows from one table even when there is no matching row in the other table.
- In Oracle syntax, `(+)` is placed on the side of the table that may have missing NULL values.
- Outer Joins are essential when you need to include records that have no corresponding match.

---

# Q6. Non-Equi Join — Job Grades and Salaries

**Problem Statement**

The HR department needs a report on job grades and salaries. First show the structure of the SALGRADE table. Then create a query that displays the name, job, department name, salary, and grade for all employees.

**SQL Query**

```sql
-- Step 1: Show structure of SALGRADE table
DESC SALGRADE;

-- Step 2: Query with Non-Equi Join
SELECT E.ENAME, E.JOB, D.DNAME, E.SAL, S.GRADE
FROM EMP E, DEPT D, SALGRADE S
WHERE E.DEPTNO = D.DEPTNO
AND E.SAL BETWEEN S.LOSAL AND S.HISAL;
```

**Explanation**

- `DESC SALGRADE` shows the structure of the SALGRADE table with columns GRADE, LOSAL, and HISAL.
- `E.DEPTNO = D.DEPTNO` is an Equi Join linking each employee to their department.
- `E.SAL BETWEEN S.LOSAL AND S.HISAL` is a Non-Equi Join that matches salary to a grade range instead of an exact value.
- Three tables EMP, DEPT, and SALGRADE are joined together in a single query.
- `GRADE` is determined by whether the employee's salary falls within a grade's low and high salary range.

**Concept Learned**

- A Non-Equi Join uses operators other than `=` such as `BETWEEN`, `<`, `>` in the join condition.
- `BETWEEN S.LOSAL AND S.HISAL` is the most common Non-Equi Join pattern for salary grading.
- Multiple tables can be joined in one query by listing all conditions in the WHERE clause.

---

# Q7. Outer Join — Departments with No Employees

**Problem Statement**

Display the ENAME and DNAME of all the employees. Also display those department names which do not have any employees working.

**SQL Query**

```sql
SELECT E.ENAME, D.DNAME
FROM EMP E, DEPT D
WHERE E.DEPTNO(+) = D.DEPTNO;
```

**Explanation**

- `(+)` is placed on `E.DEPTNO` (EMP side), making this a RIGHT OUTER JOIN so all departments are shown even with no employees.
- Departments without employees will display NULL in the ENAME column.
- In the standard EMP/DEPT schema, DEPTNO 40 (OPERATIONS) has no employees and appears with NULL ENAME.
- This is Oracle's traditional syntax for a right outer join using `(+)` on the optional side.

**Concept Learned**

- Placing `(+)` on the employee side includes all rows from the DEPT table, even those with no matching employees.
- This is useful for finding entities like departments that have no related records.
- The ANSI equivalent of this query is `RIGHT OUTER JOIN ... ON`.

---

# Q8. Self Join with Outer Join — Hired Before Their Manager

**Problem Statement**

The HR department needs to find the names and hire dates for all employees who were hired before their managers, along with their managers' names and hire dates.

**SQL Query**

```sql
SELECT E.ENAME AS "Employee", E.HIREDATE AS "Emp HireDate",
       M.ENAME AS "Manager",  M.HIREDATE AS "Mgr HireDate"
FROM EMP E, EMP M
WHERE E.MGR = M.EMPNO(+)
AND E.HIREDATE < M.HIREDATE;
```

**Explanation**

- The Self Join uses aliases `E` for employee and `M` for manager, joining on `E.MGR = M.EMPNO`.
- `M.EMPNO(+)` makes it an outer join so employees without managers are also considered.
- `E.HIREDATE < M.HIREDATE` filters only those employees who were hired before their manager.
- Both `ENAME` and `HIREDATE` are displayed for the employee and their manager side by side.
- Column aliases in double quotes display meaningful labels with spaces in the output.

**Concept Learned**

- Self Join and Outer Join can be combined in a single query to handle NULL relationships along with date comparisons.
- Date comparisons use standard operators like `<`, `>`, `=` directly on DATE columns in Oracle.
- This pattern is common for hierarchical data stored in a single table like an org chart.

---

# Q9. USING Clause — Employees Working as CLERK

**Problem Statement**

Display the EMPNO, ENAME, DNAME, and LOC of those employees who are working as CLERK. Use the USING clause.

**SQL Query**

```sql
SELECT E.EMPNO, E.ENAME, D.DNAME, D.LOC
FROM EMP E
JOIN DEPT D USING (DEPTNO)
WHERE E.JOB = 'CLERK';
```

**Explanation**

- `JOIN DEPT D USING (DEPTNO)` joins the two tables on the DEPTNO column using ANSI syntax.
- The `USING` clause requires that the column name DEPTNO exists in both tables with the same name.
- Unlike the ON clause, the join column in `USING` must not be prefixed with a table alias.
- `WHERE E.JOB = 'CLERK'` filters the result to show only employees with the CLERK job title.
- `EMPNO`, `ENAME` come from EMP; `DNAME`, `LOC` come from DEPT.

**Concept Learned**

- The `USING` clause is a shorthand for joining on a column that has the same name in both tables.
- When using `USING`, the join column DEPTNO must not be prefixed with any table alias.
- `USING` is cleaner than `ON` when column names match; `ON` is more flexible for non-matching column names.

---

# Q10. ON Clause — Employees with Salary More Than 2000

**Problem Statement**

Display the ENAME, SAL, MGR, and DNAME of employees whose salary is more than 2000. Use the ON clause.

**SQL Query**

```sql
SELECT E.ENAME, E.SAL, E.MGR, D.DNAME
FROM EMP E
JOIN DEPT D ON (E.DEPTNO = D.DEPTNO)
WHERE E.SAL > 2000;
```

**Explanation**

- `JOIN DEPT D ON (E.DEPTNO = D.DEPTNO)` explicitly specifies the join condition using the ON clause.
- The `ON` clause allows full control over the join condition and works even when column names differ between tables.
- `WHERE E.SAL > 2000` filters and shows only employees earning more than 2000.
- `ENAME`, `SAL`, `MGR` come from EMP; `DNAME` comes from DEPT.
- Table alias prefixes `E.` and `D.` are mandatory in the ON clause to avoid ambiguity.

**Concept Learned**

- The `ON` clause explicitly defines the join condition and is the most flexible join syntax in SQL.
- It supports any condition such as equality, inequality, or expressions unlike `USING` or `NATURAL JOIN`.
- `ON` handles the join condition while `WHERE` handles the filter condition and they work together cleanly.

---

# Q11. LEFT OUTER JOIN — All Employees with Department Info

**Problem Statement**

Display the EMPNO, ENAME, JOB, DEPTNO, DNAME, and LOC of employees. Use LEFT OUTER JOIN.

**SQL Query**

```sql
SELECT E.EMPNO, E.ENAME, E.JOB, E.DEPTNO, D.DNAME, D.LOC
FROM EMP E
LEFT OUTER JOIN DEPT D ON (E.DEPTNO = D.DEPTNO);
```

**Explanation**

- `LEFT OUTER JOIN` returns all rows from the left table EMP and matching rows from the right table DEPT.
- If an employee has no matching department, `DNAME` and `LOC` will be NULL in the output.
- `ON (E.DEPTNO = D.DEPTNO)` specifies the join condition between EMP and DEPT.
- All employees in the EMP table will appear in the result regardless of whether they have a department match.
- This is the ANSI SQL equivalent of Oracle's traditional `EMP.DEPTNO = DEPT.DEPTNO(+)` syntax.

**Concept Learned**

- `LEFT OUTER JOIN` returns all rows from the left table even if no match exists in the right table.
- Unmatched rows from the right table appear as NULL in the result set.
- Oracle's `(+)` on the right side achieves the same result as `LEFT OUTER JOIN` in ANSI syntax.

---

# Q12. RIGHT OUTER JOIN — All Departments Including Empty Ones

**Problem Statement**

Display the ENAME and DNAME of employees. Use RIGHT OUTER JOIN.

**SQL Query**

```sql
SELECT E.ENAME, D.DNAME
FROM EMP E
RIGHT OUTER JOIN DEPT D ON (E.DEPTNO = D.DEPTNO);
```

**Explanation**

- `RIGHT OUTER JOIN` returns all rows from the right table DEPT and matching rows from the left table EMP.
- Departments that have no employees still appear in the result with `ENAME` as NULL.
- In the standard EMP/DEPT schema, DEPTNO 40 (OPERATIONS) has no employees so it appears with NULL ENAME.
- `ON (E.DEPTNO = D.DEPTNO)` is the join condition linking employees to their departments.
- This is the ANSI equivalent of Oracle's traditional `E.DEPTNO(+) = D.DEPTNO` syntax.

**Concept Learned**

- `RIGHT OUTER JOIN` returns all rows from the right table even when there is no matching row in the left table.
- It is commonly used to find parent records like departments that have no child records like employees.
- `RIGHT OUTER JOIN` is equivalent to switching the table order and using `LEFT OUTER JOIN`.

---

# Q13. FULL OUTER JOIN — All Employees and All Departments

**Problem Statement**

Display the EMPNO, DNAME, and LOC of employees. Use FULL OUTER JOIN.

**SQL Query**

```sql
SELECT E.EMPNO, D.DNAME, D.LOC
FROM EMP E
FULL OUTER JOIN DEPT D ON (E.DEPTNO = D.DEPTNO);
```

**Explanation**

- `FULL OUTER JOIN` returns all rows from both EMP and DEPT whether or not they have a matching row in the other table.
- Employees without a matching department will have NULL for `DNAME` and `LOC`.
- Departments without any employees will have NULL for `EMPNO`.
- `ON (E.DEPTNO = D.DEPTNO)` defines the join condition between the two tables.
- This is effectively a combination of `LEFT OUTER JOIN` and `RIGHT OUTER JOIN` merged into one result.

**Concept Learned**

- `FULL OUTER JOIN` is the union of LEFT and RIGHT OUTER JOINs and includes all unmatched rows from both tables.
- It is useful when you want to see all records from both tables regardless of whether a match exists.
- Oracle does not support `FULL OUTER JOIN` using the `(+)` operator so you must use ANSI syntax.
