# Assignment 01 - Employee Table Normalization

## Question

Given relation:

EMPNO, ENAME, SAL, DEPTNO, DNAME, LOC

Suggest whether the table can be further normalized. Mention the current normal form and convert it into the next normal form.

---

## Analysis

Primary Key:

- EMPNO

Functional Dependencies:

- EMPNO → ENAME, SAL, DEPTNO
- DEPTNO → DNAME, LOC

Since DNAME and LOC depend on DEPTNO instead of EMPNO directly, a transitive dependency exists.

Therefore, the table is in **Second Normal Form (2NF)** but **not in Third Normal Form (3NF)**.

---

## Conversion to 3NF

### EMPLOYEE

| EMPNO | ENAME | SAL | DEPTNO |
|-------|-------|-----|--------|

### DEPARTMENT

| DEPTNO | DNAME | LOC |
|--------|-------|-----|

---

## Conclusion

The transitive dependency has been removed by separating department details into a different table. The resulting schema satisfies Third Normal Form (3NF).

## Concept Learned

- 1NF removes repeating groups.
- 2NF removes partial dependency.
- 3NF removes transitive dependency.
- Department information should be stored in a separate table to reduce redundancy.