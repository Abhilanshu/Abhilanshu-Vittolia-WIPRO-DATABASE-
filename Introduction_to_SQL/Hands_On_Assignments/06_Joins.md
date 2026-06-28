# Q1. Natural Join — Addresses of All Departments

**Problem Statement**

Create a report...

**SQL Query**

```sql
SELECT E.EMPNO, E.ENAME, E.SAL, D.DNAME, D.LOC
FROM EMP E
NATURAL JOIN DEPT D;
```

**Explanation**
