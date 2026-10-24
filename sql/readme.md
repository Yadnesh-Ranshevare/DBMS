# Structured Query Language (SQL)

---
# Content
1. [introduction](#introduction)
2. [Database in SQL](#database-in-sql)
3. [DataType in SQL](#datatype-in-sql)

---
# Introduction
SQL (Structured Query Language) is a standard programming language used to create, store, retrieve, update, and delete data in a relational database.

### Example

Suppose we have a table named `Students`:

| ID | Name  | Age |
| -- | ----- | --- |
| 1  | Rahul | 20  |
| 2  | Priya | 21  |
| 3  | Amit  | 19  |

To retrieve all students, we use:

```
SELECT * FROM Students;
```

Output: The query returns all rows and columns from the `Students` table.

### Main uses of SQL

1. Create — Create databases and tables.
2. Retrieve — Fetch data using `SELECT`.
3. Insert — Add new records using `INSERT`.
4. Update — Modify existing records using `UPDATE`.
5. Delete — Remove records using `DELETE`.
6. Control access — Manage database permissions.

### Common SQL commands

| Command  | Purpose                  |
| -------- | ------------------------ |
| `CREATE` | Creates database objects |
| `INSERT` | Adds new data            |
| `SELECT` | Retrieves data           |
| `UPDATE` | Modifies data            |
| `DELETE` | Deletes data             |
| `DROP`   | Removes database objects |

### Popular databases that use SQL

- MySQL
- PostgreSQL
- Microsoft SQL Server
- Oracle Database
- SQLite

In simple words: SQL is the language we use to communicate with a relational database and perform operations on its data.

[Go To Top](#content)

---
# Database in SQL
A database in SQL is organized into tables, which store data in rows and columns. A database can contain multiple tables related to each other.

### Hierarchy of SQL Database Structure

<img src="./img/database-hierarchy.png" style="width:500px"/>

### Main components

1. **Database**: A collection of organized data and database objects.
2. **Table**: Stores related data in rows and columns.
3. **Row (Record)**: Represents one complete entry in a table.
4. **Column (Field)**: Represents a particular attribute, such as name or age.
5. **Primary Key**: Uniquely identifies each row in a table.
6. **Foreign Key**: Connects related tables by referencing a key in another table.

### Example of a table

`Students` table:

| Student_ID | Name  | Age |
| ---------- | ----- | --- |
| 101        | Rahul | 20  |
| 102        | Priya | 21  |
| 103        | Amit  | 19  |

- Table name: Students
- Columns: Student_ID, Name, Age
- Rows: 3 student records
- Primary key: Student_ID

### SQL commands
1. **create the database**

    ```sql
    CREATE DATABASE CollegeDB;
    ```
2. **use the respective database**
    ```sql
    USE CollegeDB;
    ```
    Now whenever you perform any CURD operation it will be done on this database
3. **Create the table in the selected database database**
    ```sql
    CREATE TABLE Students (
        Student_ID INT PRIMARY KEY,
        Name VARCHAR(50),
        Age INT
    );
    ```
    - `CREATE TABLE` creates a table.
    - `INT` stores integer values.
    - `VARCHAR(50)` stores variable-length text up to 50 characters.
    - `PRIMARY KEY` uniquely identifies each student.
4. **Delete table from database**
    ```sql
    DROP TABLE Students
    ```
5. **Delete the database:**
    ```sql
    DROP DATABASE CollegeDB;
    ```


[Go To Top](#content)

---
# DataType in SQL

SQL data types define the type of values that can be stored in a table column, such as numbers, text, dates, or Boolean values.


### 1. Numeric Data Types

Used to store numbers.

| Data Type      | Description                                       | Example                  |
| -------------- | ------------------------------------------------- | ------------------------ |
| `INT`          | Stores integers                                   | `25`                     |
| `SMALLINT`     | Stores small-range integers                       | `100`                    |
| `BIGINT`       | Stores large-range integers                       | `9876543210`             |
| `DECIMAL(p,s)` | Stores exact decimal numbers                      | `DECIMAL(5,2)` → `99.99` |
| `FLOAT`        | Stores approximate decimal numbers                | `3.14159`                |
| `REAL`         | Stores approximate numbers with limited precision | `3.14`                   |

### 2. String Data Types

Used to store text and characters.

| Data Type    | Description            | Example                   |
| ------------ | ---------------------- | ------------------------- |
| `CHAR(n)`    | Fixed-length string    | `'ABC'`                   |
| `VARCHAR(n)` | Variable-length string | `'Rahul'`                 |
| `TEXT`       | Stores long text       | `'This is a description'` |

CHAR vs VARCHAR

| CHAR                           | VARCHAR                          |
| ------------------------------ | -------------------------------- |
| Fixed-length string            | Variable-length string           |
| Suitable for fixed-size values | Suitable for varying-length text |
| Example: `CHAR(10)`            | Example: `VARCHAR(50)`           |



### 3. Date and Time Data Types

Used to store dates and time values.

| Data Type   | Description                                          | Example                 |
| ----------- | ---------------------------------------------------- | ----------------------- |
| `DATE`      | Stores date                                          | `'2026-10-24'`          |
| `TIME`      | Stores time                                          | `'14:30:00'`            |
| `DATETIME`  | Stores date and time                                 | `'2026-10-24 14:30:00'` |
| `TIMESTAMP` | Stores a timestamp; behavior depends on the database | `'2026-10-24 14:30:00'` |

### 4. Boolean Data Type

| Data Type | Description              | Example         |
| --------- | ------------------------ | --------------- |
| `BOOLEAN` | Represents true or false | `TRUE`, `FALSE` |

Note: Support and storage behavior vary across databases. For example, MySQL treats `BOOLEAN` as a synonym for `TINYINT(1)`, while PostgreSQL has a native Boolean type.

### 5. Binary Data Types

Used to store binary data.

| Data Type      | Description                                   |
| -------------- | --------------------------------------------- |
| `BINARY(n)`    | Fixed-length binary data                      |
| `VARBINARY(n)` | Variable-length binary data                   |
| `BLOB`         | Binary large object, such as an image or file |



> [check out this](https://www.w3schools.com/sql/sql_datatypes.asp) to know more datatype

[Go To Top](#content)

---
