# Assignment 02 - Student Table Normalization

## Question

Given relation:

ROLLNO, NAME, AGE, EXAM, MARKS, GRADE

Suggest whether the table can be further normalized. Mention the current normal form and convert it into the next normal form.

---

## Analysis

Composite Primary Key:

- (ROLLNO, EXAM)

Functional Dependencies:

- ROLLNO → NAME, AGE
- (ROLLNO, EXAM) → MARKS
- MARKS → GRADE

Since NAME and AGE depend only on ROLLNO (part of the composite key), the table contains a partial dependency.

Therefore, the table is in **First Normal Form (1NF)** but **not in Second Normal Form (2NF)**.

---

## Conversion to 2NF

### STUDENT

| ROLLNO | NAME | AGE |
|--------|------|-----|

### RESULT

| ROLLNO | EXAM | MARKS | GRADE |
|--------|------|-------|-------|

---

## Conclusion

The partial dependency has been removed by separating student details from examination details. The resulting schema satisfies Second Normal Form (2NF).

---

## Concept Learned

- Composite keys consist of two or more attributes.
- Partial dependency occurs when a non-key attribute depends on only part of a composite primary key.
- 2NF eliminates partial dependencies.