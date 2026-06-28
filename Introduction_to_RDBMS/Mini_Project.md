# Mini Project - Normalization

## Question 1

### Objective

Normalize the given table into First Normal Form (1NF).

### Given Table

| Member_Id | First_Name | Last_Name | Hobbies |
|-----------|------------|-----------|---------|
|101|Jayson|Mark|Cricket,Swimming,Football|
|102|Ram|Ganesh|Swimming,Running,Music|
|103|Raj|Kishore|Dancing,Singing,Running|

---

## Analysis

The **Hobbies** column contains multiple values in a single cell, which violates the First Normal Form (1NF). According to 1NF, each attribute should contain only atomic (single) values.

---

## Solution (1NF)

| Member_Id | First_Name | Last_Name | Hobby |
|-----------|------------|-----------|-------|
|101|Jayson|Mark|Cricket|
|101|Jayson|Mark|Swimming|
|101|Jayson|Mark|Football|
|102|Ram|Ganesh|Swimming|
|102|Ram|Ganesh|Running|
|102|Ram|Ganesh|Music|
|103|Raj|Kishore|Dancing|
|103|Raj|Kishore|Singing|
|103|Raj|Kishore|Running|

---

## Conclusion

The repeating values in the Hobbies column have been separated into individual rows. The table now satisfies the requirements of First Normal Form (1NF).

# Question 2

## Objective

Normalize the given table into Second Normal Form (2NF).

### Given Table

| EmpNo | Training | Training_Date | Dept |
|-------|----------|---------------|------|
|101|Oracle SQL|12-Aug-2015|TT|
|101|Java|21-Aug-2015|BU|
|102|Oracle SQL|18-Sep-2014|TT|

---

## Analysis

Composite Primary Key:

- (EmpNo, Training)

Functional Dependencies:

- (EmpNo, Training) → Training_Date
- EmpNo → Dept

Since **Dept** depends only on **EmpNo**, which is part of the composite primary key, the table contains a **partial dependency**.

Therefore, the table is in **First Normal Form (1NF)** but **not in Second Normal Form (2NF)**.

---

## Solution (2NF)

### EMPLOYEE

| EmpNo | Dept |
|-------|------|
|101|TT|
|102|TT|

### EMPLOYEE_TRAINING

| EmpNo | Training | Training_Date |
|-------|----------|---------------|
|101|Oracle SQL|12-Aug-2015|
|101|Java|21-Aug-2015|
|102|Oracle SQL|18-Sep-2014|

---

## Conclusion

The partial dependency has been removed by separating employee details from training details. The resulting schema satisfies Second Normal Form (2NF).

# Question 3

## Objective

Normalize the given table into Third Normal Form (3NF).

### Given Table

| Member_Id | First_Name | Last_Name | Sports | Fees |
|-----------|------------|-----------|--------|------|
|101|Rajesh|Chand|Cricket|100|
|102|Jayesh|Raj|Hockey|80|
|103|Mark|Dorson|Football|90|

---

## Analysis

Primary Key:

- Member_Id

Functional Dependencies:

- Member_Id → First_Name, Last_Name, Sports
- Sports → Fees

Since **Fees** depends on **Sports** instead of directly on **Member_Id**, the table contains a **transitive dependency**.

Therefore, the table is in **Second Normal Form (2NF)** but **not in Third Normal Form (3NF)**.

---

## Solution (3NF)

### MEMBER

| Member_Id | First_Name | Last_Name | Sports |
|-----------|------------|-----------|--------|
|101|Rajesh|Chand|Cricket|
|102|Jayesh|Raj|Hockey|
|103|Mark|Dorson|Football|

### SPORTS

| Sports | Fees |
|--------|------|
|Cricket|100|
|Hockey|80|
|Football|90|

---

## Conclusion

The transitive dependency has been removed by separating sports details into a different table. The resulting schema satisfies Third Normal Form (3NF).