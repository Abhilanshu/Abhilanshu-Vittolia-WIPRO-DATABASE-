# Assignment 03 - Employee Project Table Normalization

## Question

Given relation:

EMPNO, PROJECT_NO, NO_OF_DAYS, CUSTOMERNAME

Primary Key: (EMPNO, PROJECT_NO)

Identify the problem in the table and normalize it.

---

## Analysis

Composite Primary Key:

- (EMPNO, PROJECT_NO)

Functional Dependencies:

- (EMPNO, PROJECT_NO) → NO_OF_DAYS
- PROJECT_NO → CUSTOMERNAME

Since CUSTOMERNAME depends only on PROJECT_NO (part of the composite primary key), the table contains a partial dependency.

Therefore, the table is in **First Normal Form (1NF)** but **not in Second Normal Form (2NF)**.

---

## Conversion to 2NF

### EMPLOYEE_PROJECT

| EMPNO | PROJECT_NO | NO_OF_DAYS |
|--------|------------|------------|

### PROJECT

| PROJECT_NO | CUSTOMERNAME |
|------------|--------------|

---

## Conclusion

The partial dependency has been removed by separating project details into a different table. The resulting schema satisfies Second Normal Form (2NF).

---

## Concept Learned

- A composite primary key consists of two or more attributes.
- Partial dependency occurs when a non-key attribute depends on only part of the composite key.
- 2NF removes partial dependencies by decomposing the relation into smaller tables.