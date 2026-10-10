# Relational Model
---

# Content
1. [Introduction](#introduction)
2. [Relational Model vs ER Model](#relational-model-vs-er-model)
3. [Relational Model is a Complete Model](#relational-model-is-a-complete-model)
4. [Relationship In Relational Model](#relationship-in-relational-model)

---

# Introduction
The Relational Model is a database model in which data is stored in the form of tables (relations) consisting of rows and columns.

It was proposed by E. F. Codd in 1970 and is the foundation of relational database systems such as MySQL, PostgreSQL, Oracle, and SQL Server.

RDBMS (Relational Database Management System) are the DBMS designed for for database that follow the relational model

### Relational Model vs. Relational Database

These terms are related but not identical.

- **Relational model:** The theoretical framework that defines how data is represented and related.
- **Relational database:** An actual database system that implements relational concepts, such as MySQL or PostgreSQL.


Example of RDBMS: Oracle, MySQL, PostgreSQL, SQLite

### Example of a Relational Model

Suppose we have a `Student` table:

| Student_ID | Name  | Age | City   |
| ---------- | ----- | --- | ------ |
| 101        | Rahul | 20  | Mumbai |
| 102        | Priya | 21  | Pune   |
| 103        | Amit  | 19  | Nashik |

In the relational model:

- **Tuple**: A row representing one student.
- **Attribute**: A column, such as `Name` or `Age`.
- **Domain**: The set of valid values an attribute can contain. For example, `Age` should contain valid age values.
- **Degree**: The number of attributes (columns). Here, it is 4.
- **Cardinality**: The number of tuples (rows). Here, it is 3.

###  Keys in the Relational Model

Keys help identify records and establish relationships between tables.

| Key           | Meaning                                                                                  |
| ------------- | ---------------------------------------------------------------------------------------- |
| Primary Key   | Uniquely identifies each row; cannot be NULL.                                            |
| Candidate Key | A minimal set of attributes capable of uniquely identifying a row.                       |
| Foreign Key   | An attribute that references a candidate key, usually the primary key, in another table. |
| Super Key     | Any set of attributes that uniquely identifies a row.                                    |
| Alternate Key | A candidate key that was not selected as the primary key.                                |
| Surrogate Key | Artificially generated key used to uniquely identify each record in a table. It has no business meaning and is created specifically for identification purposes. | 

For example, `Student_ID` can be the primary key of the `Student` table.

Suppose we also have a `Department` table. Its `Department_ID` could be referenced by a foreign key in the `Student` table to associate each student with a department.

### Properties of the Relational Model

1. Data is organized into tables.
2. Each row represents a record.
3. Each column represents an attribute.
4. Each attribute has a defined domain.
5. A primary key uniquely identifies each row.
6. Relationships between tables can be established using foreign keys.
7. Relational operations can retrieve and manipulate data.

### Advantages

- Simple and easy to understand.
- Reduces data duplication through proper database normalization.
- Maintains data integrity using constraints and keys.
- Supports flexible data retrieval using SQL.
- Makes it easier to connect related data across tables.

### Conclusion
The relational model is a database model proposed by E. F. Codd in 1970. It represents data in the form of tables consisting of rows and columns. Rows are called tuples, columns are called attributes, and relationships between tables are established using keys such as primary keys and foreign keys. It provides data integrity, reduces redundancy through normalization, and allows data to be manipulated using SQL.


[Go To Top](#content)

---
# Relational Model vs ER Model

The ER Model (Entity-Relationship Model) is used to design a database conceptually, while the Relational Model is used to represent data in tables.

> ER model is not a complete model whereas a relational model is a complete model

### Key Differences

| Basis           | ER Model                                         | Relational Model                                                 |
| --------------- | ------------------------------------------------ | ---------------------------------------------------------------- |
| Purpose         | Database design and planning                     | Database structure and data storage                              |
| Representation  | Entities, attributes, relationships              | Tables, rows, columns                                            |
| Main components | Entity, Attribute, Relationship                  | Relation, Tuple, Attribute                                       |
| Diagram         | ER diagram                                       | Tables or relational schemas                                     |
| Relationships   | Represented using relationship lines or diamonds | Represented using primary and foreign keys                       |
| Keys            | Identifies entities uniquely                     | Identifies rows and connects tables                              |
| Stage           | Mainly conceptual design                         | Logical database design and implementation                       |
| Example         | Student enrolls in Course                        | `Student` and `Course` tables linked through an enrollment table |

### Example

Suppose you are designing a college database.

- **ER Model**
    ```
    ┌────────────────────────────┐                            ┌───────────────────────────┐
    │ STUDENT (Student_ID, Name) │────── Enrolls_in ────────> │ COURSE (Course_ID, Title) │
    └────────────────────────────┘                            └───────────────────────────┘
    ```

    The ER model tells us that students enroll in courses. It describes what entities exist and how they relate.

- **Relational Model**

    - Student table:

        | Student_ID (PK) | Name  |
        | --------------- | ----- |
        | 101             | Rahul |
        | 102             | Priya |

    - Course table:

        | Course_ID (PK) | Title  |
        | -------------- | ------ |
        | C1             | Java   |
        | C2             | Python |

    - Enrollment table:

        | Student_ID (FK) | Course_ID (FK) |
        | --------------- | -------------- |
        | 101             | C1             |
        | 101             | C2             |
        | 102             | C1             |

    Here, the many-to-many relationship is represented through a separate `Enrollment` table containing foreign keys.

### How Are They Related?

The ER model is used for conceptual database design, which is then converted into a relational schema consisting of tables and keys, and finally implemented in an SQL database using commands such as `CREATE TABLE` and constraints.


> The ER model is a conceptual database model that represents entities, attributes, and relationships using an ER diagram. The relational model represents data using tables consisting of rows and columns, with primary and foreign keys used to identify records and establish relationships. In database design, the ER model is generally used first, and it is then converted into a relational schema for implementation.
>
>Quick memory trick: ER model = Design the database. Relational model = Represent the data in tables.


[Go To Top](#content)

---

# Relational Model is a Complete Model

We have learned that for any data model to be complete, it must answer three basic questions:

1. **Storage:** How is the data stored?
2. **Data Manipulation Language:** How can we manipulate the data?
3. **Integrity Constraints:** What restrictions ensure data is correct?

### ER Model is Not a Complete Model

The ER model is not considered a complete implementation-level data model because it does not specify the actual storage format or a data manipulation language.

It is primarily a conceptual/design model used to describe the structure of a database at a high level.

> ER Model = Conceptual blueprint of the database, not the complete implementation-level data model.

### How the Relational Model is a Complete Model?

The relational model addresses all three requirements needed for a complete data model:

1. **Storage Format:** Data is stored in the form of tables (relations), consisting of rows (tuples) and columns (attributes).

2. **Data Manipulation Language:** Relational algebra and relational calculus provide formal operations to retrieve and manipulate data. SQL is a widely used language for implementing these operations in relational database systems.

3. **Integrity Constraints:** Rules ensure the accuracy, consistency, and validity of data. The main types include:
   - **Domain Integrity:** Ensures that column values belong to a valid domain. Example: Age cannot be negative.
   - **Entity Integrity:** Ensures that a primary key cannot be NULL.
   - **Referential Integrity:** Ensures that a foreign key references an existing record in the referenced table, unless NULL is allowed.
   - **Key Constraints:** Ensure that key values uniquely identify records. Example: Two students cannot have the same Student_ID if it is a primary or candidate key.

**Conclusion:** The relational model is considered a complete data model because it defines how data is structured, how it can be manipulated, and what constraints maintain its integrity.


### Why we use ER model?
whenever we design the database it done in two parts:

1. design ER model
2. convert ER model into relational model

where:
- each and every entity type (strong / weak) is directly converted into table along with its simple attributes
- for multi valued attribute we can use another table with a reference to main table via foreign key
- whereas in case of composite attribute we can store it in main table directly


[Go To Top](#content)

---
# Relationship In Relational Model
In ER model a relationship describes the association between two or more entities.

For example:
```
Student ───── Enrolls in ───── Course
```
Here:
- Student → Entity
- Course → Entity
- Enrolls in → Relationship


When converting an ER model into a relational model, we represent relationships using foreign keys or separate tables, depending on the type of relationship.

### There are 3 main types of relationships:

1. **One-to-One (1:1)**

    - Example: One person has one passport, and each passport belongs to one person.

        ```
        person ──1── has ──1─── passport
        ```

    - Conversion: Add the primary key of one table as a foreign key in the other table. Apply a `UNIQUE` constraint to enforce the one-to-one relationship.

2. **One-to-Many (1:N)**

    - Example: One department has many students, but each student belongs to one department.

        ```
        department ──1── has ──N─── student
        ```
    - Conversion: Add the primary key of the one side (department) as a foreign key in the many side (student).

3. **Many-to-Many (M:N)**

    - Example: A student can enroll in many courses, and a course can have many students.

        ```
        Student ──M── enrolls in ──N── Course
        ```

    - Conversion: Create a new table for the relationship and include the primary keys of both entities as foreign keys. They commonly form a composite primary key.

### In Case of Total vs Partial Participation

Participation constraints specify whether the participation of an entity in a relationship is mandatory or optional.

There are two types of participation:

**1. Total Participation**

- Every entity must participate in at least one instance of the relationship.
- Represented by a **double line** in an ER diagram.
- **Conversion:** When the foreign key is stored in the participating entity's table, it is generally declared `NOT NULL` to ensure mandatory participation.

**Example:** Every student must belong to a department.

ER Model:
```text
Student ═════ Belongs to ───── Department
```

Relational Model:
- `Department(Dept_ID PK, Dept_Name)`
- `Student(Student_ID PK, Name, Dept_ID FK NOT NULL)`
> PK = primary key\
> FK = foreign Key

Here, `Dept_ID NOT NULL` ensures that every student is assigned a department.

**2. Partial Participation**

- Only some entities participate in the relationship; others may not participate.
- Represented by a **single line** in an ER diagram.
- **Conversion:** When the foreign key is stored in the participating entity's table, it may be declared `NULL` to allow optional participation.

**Example:** A student may or may not join a club.

ER Model:
```text
Student ───── Joins ───── Club
```

Relational Model:
- `Student(Student_ID PK, Name, Club_ID FK NULL)`

Here, `Club_ID` can be `NULL`, allowing a student to exist without joining a club. This example assumes each student can join at most one club.

### Difference Between Total and Partial Participation

| Total Participation | Partial Participation |
|---|---|
| Participation is mandatory. | Participation is optional. |
| Represented by a double line. | Represented by a single line. |
| Foreign key generally uses `NOT NULL` when stored on the participating side. | Foreign key may allow `NULL` when participation is optional. |
| Example: Every student must belong to a department. | Example: A student may or may not join a club. |

**Important Note:** For a many-to-many relationship, a separate relationship table is created regardless of participation. A foreign key alone does not enforce total participation in such a relationship; additional constraints may be required.

[Go To Top](#content)

---

