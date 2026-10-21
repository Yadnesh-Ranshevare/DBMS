# Normalization

---
# Content
1. [introduction](#introduction)
2. [Insertion Anomaly in DBMS](#insertion-anomaly-in-dbms)
3. [Deletion Anomaly in DBMS](#deletion-anomaly-in-dbms)
4. [Update Anomaly in DBMS](#update-anomaly-in-dbms)
5. [Data Integrity](#data-integrity)
6. [First Normal Form (1NF)](#first-normal-form-1nf)
7. [Second Normal Form (2NF)](#second-normal-form-2nf)
8. [Third Normal Form (3NF)](#third-normal-form-3nf)
9. [Fourth Normal Form (4NF)](#fourth-normal-form-4nf)
10. [Fifth Normal Form (5NF)](#fifth-normal-form-5nf)
11. [Comparison of 1NF, 2NF, 3NF, 4NF and 5NF](#comparison-of-1nf-2nf-3nf-4nf-and-5nf)

---
# Introduction 

Normalization is the process of organizing data in a database to reduce data redundancy (duplicate data) and prevent data anomalies during insertion, updating, and deletion.

It divides large tables into smaller, related tables and establishes relationships between them using keys.

### Example

Consider an unnormalized table:

| Student_ID | Student_Name | Course |
| ---------- | ------------ | ------ |
| 1          | Rahul        | Java   |
| 1          | Rahul        | Python |
| 2          | Amit         | Java   |

Here, Rahul's name is repeated because he is enrolled in multiple courses.

After normalization, we can divide the data into two tables.

Student Table

| Student_ID (PK) | Student_Name |
| --------------- | ------------ |
| 1               | Rahul        |
| 2               | Amit         |

Enrollment Table

| Student_ID (FK) | Course |
| --------------- | ------ |
| 1               | Java   |
| 1               | Python |
| 2               | Java   |

This reduces unnecessary repetition and organizes the data better.

### Objectives of Normalization

1. To reduce data redundancy.
2. To maintain data consistency and integrity.
3. To prevent insertion, update, and deletion anomalies.
4. To organize data into properly structured tables.
5. To establish relationships between tables.

### Types of Normalization

| Normal Form                   | Description                                                                                         |
| ----------------------------- | --------------------------------------------------------------------------------------------------- |
| 1NF (First Normal Form)       | Each cell contains a single, atomic value, with no repeating groups.                                |
| 2NF (Second Normal Form)      | It is in 1NF and has no partial dependency on a composite candidate key.                            |
| 3NF (Third Normal Form)       | It is in 2NF and has no transitive dependency of non-key attributes on candidate keys.              |
| BCNF (Boyce-Codd Normal Form) | For every non-trivial functional dependency $X \rightarrow Y$, $X$ must be a superkey.      |
| 4NF (Fourth Normal Form)      | It is in BCNF and has no non-trivial multivalued dependencies unless the determinant is a superkey. |
| 5NF (Fifth Normal Form)       | It eliminates non-trivial join dependencies that are not implied by candidate keys.                 |

In short: Normalization helps create an efficient, consistent database by minimizing unnecessary data duplication and avoiding data anomalies.

[Go To Top](#content)

---
# Insertion Anomaly in DBMS

Insertion anomaly occurs when we cannot insert new data into a database without adding some unrelated or unnecessary data.

It happens when multiple types of information are stored in a single table, causing unnecessary dependencies.

### Example

Consider the following table:

| Student_ID | Student_Name | Course |
| ---------- | ------------ | ------ |
| 101        | Rahul        | Java   |
| 102        | Amit         | Python |

Suppose we want to add a new course, SQL, but no student has enrolled in it yet.

We cannot insert the course without providing a student ID and name because all the information is stored in the same table. This is an insertion anomaly.

### How to Prevent It?

We can normalize the database by dividing it into separate tables:

Student Table

| Student_ID | Student_Name |
| ---------- | ------------ |
| 101        | Rahul        |
| 102        | Amit         |

Course Table

| Course_ID | Course_Name |
| --------- | ----------- |
| C1        | Java        |
| C2        | Python      |
| C3        | SQL         |

Now, we can insert a new course without requiring any student information.

In short: Insertion anomaly occurs when we cannot insert certain data without inserting additional, unrelated data. Normalization helps prevent it by separating different types of information into appropriate tables.


[Go To Top](#content)

---
# Deletion Anomaly in DBMS

Deletion anomaly occurs when deleting a record unintentionally causes the loss of other important information stored in the same table.

It happens when multiple types of information are stored together in a single table.

### Example

Consider the following table:

| Student_ID | Student_Name | Course |
| ---------- | ------------ | ------ |
| 101        | Rahul        | Java   |
| 102        | Amit         | Python |
| 103        | Priya        | SQL    |

Suppose Priya is the only student enrolled in SQL. If we delete Priya's record, we also lose the information that the SQL course exists.

This is called a deletion anomaly.

### How to Prevent It?

We can normalize the database by separating student and course information into different tables.

Student Table

| Student_ID | Student_Name |
| ---------- | ------------ |
| 101        | Rahul        |
| 102        | Amit         |
| 103        | Priya        |

Course Table

| Course_ID | Course_Name |
| --------- | ----------- |
| C1        | Java        |
| C2        | Python      |
| C3        | SQL         |

Now, deleting Priya's student record will not delete the SQL course information.

In short: Deletion anomaly occurs when deleting one record unintentionally removes other valuable information. Normalization helps prevent it by separating independent data into different tables.

[Go To Top](#content)

---

# Update Anomaly in DBMS

Update anomaly occurs when the same information is stored in multiple rows, and updating it in one row but not in the others causes data inconsistency.

It happens due to data redundancy in a database table.

### Example

Consider the following table:

| Student_ID | Student_Name | Course | Instructor |
| ---------- | ------------ | ------ | ---------- |
| 101        | Rahul        | Java   | Amit       |
| 102        | Priya        | Python | Neha       |
| 103        | Raj          | Java   | Amit       |

Suppose the Java instructor, Amit, changes his name to a different name due to a correction in the database.

We must update the instructor's name in both rows where the course is Java. If we update only one row, the database will contain inconsistent information.

This is called an update anomaly.

### How to Prevent It?

We can normalize the database by separating course and instructor information into different tables.

Course Table

| Course_ID | Course_Name | Instructor |
| --------- | ----------- | ---------- |
| C1        | Java        | Amit       |
| C2        | Python      | Neha       |

Now, the instructor's information is stored in one place. Updating it there avoids inconsistencies caused by repeated entries.

### In short

Update anomaly occurs when the same data must be updated in multiple places, potentially leading to inconsistent values. Normalization reduces data redundancy and helps prevent update anomalies.


[Go To Top](#content)

---
# Data Integrity

Data Integrity is the accuracy, consistency, and reliability of data stored in a database throughout its lifecycle.

It ensures that data remains correct, valid, and consistent when it is inserted, updated, or deleted.

### Types of Data Integrity

1. Entity Integrity: Ensures that each row is uniquely identified using a primary key. A primary key cannot contain `NULL` values.

2. Referential Integrity: Ensures that a foreign key refers to an existing record in the referenced table, or is `NULL` when permitted.

3. Domain Integrity: Ensures that values in a column follow the defined data type, range, and constraints.

4. User-Defined Integrity: Enforces specific business rules defined by the user or organization.

### Example

Consider a `Student` table:

| Student_ID (PK) | Name  | Age |
| --------------- | ----- | --- |
| 101             | Rahul | 20  |
| 102             | Amit  | 21  |

- Entity integrity: Two students cannot have the same primary key.
- Domain integrity: Age must satisfy the defined data type and constraints, such as `CHECK (Age >= 18)`.
- Referential integrity: If a student references a department, that department must exist in the Department table, unless `NULL` is permitted.
- User-defined integrity: A college may require students to have at least 75% attendance to be eligible for an examination.

In short: Data integrity ensures that database data remains accurate, valid, consistent, and reliable.


### How Does Normalization Maintain Data Integrity?

Normalization maintains data integrity by reducing data redundancy, organizing data into related tables, and preventing insertion, update, and deletion anomalies.

1. Reduces Data Redundancy
    - Normalization avoids storing the same information repeatedly, reducing the chance of inconsistent values.
    - Example: If a student's name is stored in multiple rows, changing it in only some rows can cause inconsistency. Normalization stores student details in one place.

2. Prevents Update Anomalies
    - When data is stored in multiple places, updating every occurrence can be difficult. Normalization reduces this problem by storing each fact in an appropriate table.

3. Prevents Insertion Anomalies
    - Normalization allows certain information to be stored independently without requiring unrelated information to be inserted at the same time.

4. Prevents Deletion Anomalies
    - Normalization prevents deleting one record from accidentally removing other important information stored in the same row.

5. Maintains Consistency Through Relationships
    - Normalized tables use primary keys and foreign keys to establish relationships. These constraints help ensure that records reference valid data.
    - Example: A `Student` table stores student details, while a `Course` table stores course details. An `Enrollment` table connects them using foreign keys.

### Conclusion

Normalization improves data integrity by minimizing duplication, preventing data anomalies, and organizing related data into properly structured tables. However, constraints such as primary keys, foreign keys, `UNIQUE`, and `CHECK` are also necessary to enforce data validity.

[Go To Top](#content)

---
# First Normal Form (1NF)

First Normal Form (1NF) is the first level of database normalization. A table is in 1NF if every cell contains a single, atomic value and there are no repeating groups or multivalued attributes.

### Rules of 1NF

1. Each cell must contain only one value.
2. Each column must contain values of a single domain (same type of data).
3. Each row must be uniquely identifiable, typically using a primary key.
4. There must be no repeating groups or multivalued attributes.

### Example

Table not in 1NF

| Student_ID | Name  | Subjects     |
| ---------- | ----- | ------------ |
| 101        | Rahul | Java, Python |
| 102        | Amit  | C, SQL       |

Here, the `Subjects` column contains multiple values in a single cell, violating 1NF.

Table in 1NF

Student:

| Student_ID | Name  |
| ---------- | ----- |
| 101        | Rahul |
| 102        | Amit  |

Subject:
| Student_ID | Subject |
| ---------- | ------- |
| 101        | Java    |
| 101        | Python  |
| 102        | C       |
| 102        | SQL     |

Now, each cell contains a single value, so the table satisfies 1NF.

In short: 1NF ensures that every cell contains a single, atomic value and eliminates repeating groups in a table.


[Go To Top](#content)

---
# Second Normal Form (2NF)

Second Normal Form (2NF) is a level of database normalization in which a table is already in 1NF and has no partial dependency of non-prime attributes on any candidate key.

> non-prime attributes: any column or field in a relation (table) that does not form part of any candidate key

In simple words, every non-key attribute must depend on the whole candidate key, not just a part of it.

### Rules of 2NF

1. The table must be in 1NF.
2. It must have no partial functional dependencies.

### Example

Consider the following table:

| Student_ID | Course_ID | Student_Name | Course_Name |
| ---------- | --------- | ------------ | ----------- |
| 101        | C1        | Rahul        | Java        |
| 101        | C2        | Rahul        | Python      |
| 102        | C1        | Amit         | Java        |

Here, the composite primary key is `(Student_ID, Course_ID)`.

However:

- `Student_ID → Student_Name` — the student's name depends only on `Student_ID`.
- `Course_ID → Course_Name` — the course name depends only on `Course_ID`.

These are partial dependencies because the non-key attributes depend on only part of the composite key. Therefore, the table violates 2NF.

### Conversion to 2NF

Separate the table into three tables.

1\. Student Table

| Student_ID (PK) | Student_Name |
| --------------- | ------------ |
| 101             | Rahul        |
| 102             | Amit         |

2\. Course Table

| Course_ID (PK) | Course_Name |
| -------------- | ----------- |
| C1             | Java        |
| C2             | Python      |

3\. Enrollment Table

| Student_ID (PK, FK) | Course_ID (PK, FK) |
| ------------------- | ------------------ |
| 101                 | C1                 |
| 101                 | C2                 |
| 102                 | C1                 |

Now, each non-key attribute depends on the whole key of its table, and the partial dependencies have been eliminated.

### In short

2NF = 1NF + No partial dependency.

Note: Partial dependency is possible only when a candidate key contains multiple attributes. A table with only single-attribute candidate keys is automatically in 2NF if it satisfies 1NF.



[Go To Top](#content)

---
# Third Normal Form (3NF)

Third Normal Form (3NF) is a level of database normalization in which a table is already in 2NF and has no transitive dependency of non-prime attributes on any candidate key.

> non-prime attributes: any column or field in a relation (table) that does not form part of any candidate key

In simple words, non-key attributes should depend on the key, the whole key, and nothing but the key.

> Boyes-codd Normal form:\
> Every attribute in a table should depend on the key, the whole key, and nothing but key.

### Rules of 3NF

1. The table must be in 2NF.
2. It must have no transitive dependency of non-prime attributes on a candidate key.

### Example

Consider the following table:

| Student_ID (PK) | Student_Name | Dept_ID | Dept_Name |
| --------------- | ------------ | ------- | --------- |
| 101             | Rahul        | D1      | IT        |
| 102             | Amit         | D2      | Computer  |
| 103             | Priya        | D1      | IT        |

Here, the functional dependencies are:

- `Student_ID → Student_Name, Dept_ID`
- `Dept_ID → Dept_Name`

Therefore, `Student_ID → Dept_Name` indirectly through `Dept_ID`.

This is called transitive dependency, so the table violates 3NF.

### Conversion to 3NF

Divide the table into two tables.

1\. Student Table

| Student_ID (PK) | Student_Name | Dept_ID (FK) |
| --------------- | ------------ | ------------ |
| 101             | Rahul        | D1           |
| 102             | Amit         | D2           |
| 103             | Priya        | D1           |

2\. Department Table

| Dept_ID (PK) | Dept_Name |
| ------------ | --------- |
| D1           | IT        |
| D2           | Computer  |

Now, department information is stored separately, eliminating the transitive dependency in the original table.

### Advantages of 3NF

1. Reduces data redundancy.
2. Prevents insertion, update, and deletion anomalies.
3. Improves data consistency and integrity.
4. Makes database maintenance easier.

In short: 3NF = 2NF + No transitive dependency of non-prime attributes on candidate keys.



[Go To Top](#content)

---
# Fourth Normal Form (4NF)

Fourth Normal Form (4NF) is a level of database normalization in which a table is in BCNF and has no non-trivial multivalued dependencies unless the determinant is a superkey.

In simple words, 4NF prevents storing two or more independent multivalued facts about the same entity in one table.

### Rules of 4NF

1. The table must be in BCNF.
2. It must not contain non-trivial multivalued dependencies unless the determinant is a superkey.

### Example

Consider the following table, where a student can have multiple hobbies and know multiple languages independently.

| Student | Hobby   | Language |
| ------- | ------- | -------- |
| Rahul   | Cricket | English  |
| Rahul   | Cricket | Hindi    |
| Rahul   | Music   | English  |
| Rahul   | Music   | Hindi    |

Here:

- Rahul has two hobbies: Cricket and Music.
- Rahul knows two languages: English and Hindi.
- Hobbies and languages are independent of each other.

This creates unnecessary combinations of values in the table.

The multivalued dependencies are:

- `Student →→ Hobby`
- `Student →→ Language`

Therefore, the table violates 4NF because `Student` is not a superkey.

### Conversion to 4NF

Divide the table into two separate tables.

1\. Student_Hobby Table

| Student | Hobby   |
| ------- | ------- |
| Rahul   | Cricket |
| Rahul   | Music   |

2\. Student_Language Table

| Student | Language |
| ------- | -------- |
| Rahul   | English  |
| Rahul   | Hindi    |

Now, hobbies and languages are stored independently, eliminating the multivalued dependency problem.

### Advantages of 4NF

1. Reduces unnecessary data redundancy.
2. Prevents insertion, update, and deletion anomalies caused by independent multivalued facts.
3. Improves data consistency.
4. Simplifies database maintenance.

In short: 4NF = BCNF + No non-trivial multivalued dependency unless its determinant is a superkey.

[Go To Top](#content)

---
# Fifth Normal Form (5NF)

Fifth Normal Form (5NF), also called Project-Join Normal Form (PJNF), is a level of database normalization in which every non-trivial join dependency is implied by the candidate keys.

In simple words, 5NF eliminates redundancy that occurs when a table can be decomposed into smaller tables and reconstructed using joins without losing information.

### Rules of 5NF

1. The table must be in 4NF.
2. Every non-trivial join dependency must be implied by the candidate keys.

### Example

Consider a table representing which suppliers supply which parts to which projects.

Supplier_Part_Project Table

| Supplier | Part | Project |
| -------- | ---- | ------- |
| S1       | P1   | J1      |
| S1       | P2   | J1      |
| S1       | P1   | J2      |

Suppose the business rules guarantee that a supplier can supply a part to a project whenever the corresponding supplier-part, supplier-project, and part-project relationships all exist.

The three-way relationship may then be decomposed into three tables.

### Conversion to 5NF

1\. Supplier_Part Table

| Supplier | Part |
| -------- | ---- |
| S1       | P1   |
| S1       | P2   |

2\. Supplier_Project Table

| Supplier | Project |
| -------- | ------- |
| S1       | J1      |
| S1       | J2      |

3\. Part_Project Table

| Part | Project |
| ---- | ------- |
| P1   | J1      |
| P2   | J1      |
| P1   | J2      |

These tables can be joined to reconstruct the original relationship only when the stated business rules make this decomposition lossless. Otherwise, joining them could generate extra combinations that never existed.

### Advantages of 5NF

1. Reduces redundancy caused by complex join dependencies.
2. Prevents certain insertion, update, and deletion anomalies.
3. Maintains data consistency.
4. Allows complex relationships to be represented using smaller tables.

### In short

5NF = 4NF + No non-trivial join dependencies that are not implied by candidate keys.


[Go To Top](#content)

---
# Comparison of 1NF, 2NF, 3NF, 4NF and 5NF

| Basis              | 1NF                                              | 2NF                                                         | 3NF                                                                               | 4NF                                                                          | 5NF                                                              |
| ------------------ | ------------------------------------------------ | ----------------------------------------------------------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Full Form          | First Normal Form                                | Second Normal Form                                          | Third Normal Form                                                                 | Fourth Normal Form                                                           | Fifth Normal Form                                                |
| Main Objective     | Eliminate repeating groups and multivalued cells | Eliminate partial dependencies                              | Eliminate transitive dependencies that violate 3NF                                | Eliminate problematic multivalued dependencies                               | Eliminate problematic join dependencies                          |
| Requirement        | Each cell contains an atomic value               | Must be in 1NF                                              | Must be in 2NF                                                                    | Must be in BCNF                                                              | Must be in 4NF                                                   |
| Dependency Removed | Repeating groups                                 | Partial dependency                                          | Transitive dependency                                                             | Multivalued dependency                                                       | Join dependency                                                  |
| Key Rule           | Rows should be uniquely identifiable             | Non-prime attributes must depend on the whole candidate key | For every non-trivial FD $X \to A$, $X$ is a superkey or $A$ is prime | Every non-trivial MVD $X \twoheadrightarrow Y$ has $X$ as a superkey | Every non-trivial join dependency is implied by candidate keys   |
| Redundancy Reduced | Repeated groups and multivalued cells            | Redundancy due to partial dependencies                      | Redundancy due to transitive dependencies                                         | Redundancy due to independent multivalued facts                              | Redundancy due to join dependencies                              |
| Example            | A cell contains multiple subjects                | Student name depends only on part of a composite key        | Department name depends on department ID, not directly on student ID              | A student's hobbies and languages are independent                            | Supplier-part-project relationships can be decomposed losslessly |

Quick revision trick:

- 1NF: Atomic values
- 2NF: No partial dependency
- 3NF: No transitive dependency
- 4NF: No problematic multivalued dependency
- 5NF: No problematic join dependency

Remember: Each higher normal form builds on earlier requirements, and decomposition should preserve information without introducing spurious rows.

[Go To Top](#content)

---