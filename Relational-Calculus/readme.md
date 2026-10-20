# Relational Calculus

---
# Content
1. [Introduction](#introduction)
2. [Tuple Relational Calculus (TRC)](#tuple-relational-calculus-trc)
3. [Domain Relational Calculus (DRC)](#domain-relational-calculus-drc)
4. [TRC vs DRC](#trc-vs-drc)

---
## Introduction to Relational Calculus

- Relational Calculus is a non-procedural query language used to retrieve data from a relational database. It is based on mathematical predicate logic.
- It specifies what data is required rather than how to retrieve it. The user defines conditions that the required data must satisfy, and the query returns the tuples or values that meet those conditions.
- Unlike Relational Algebra, which uses operations such as selection $(\sigma)$, projection $(\pi)$, and join $(\bowtie)$ to describe how to obtain results, Relational Calculus focuses on the conditions that define the desired result.
- It uses logical operators such as AND $(\land)$, OR $(\lor)$, NOT $(\neg)$, and quantifiers such as existential $(\exists)$ and universal $(\forall)$.
- Relational Calculus has two types:
  1. [Tuple Relational Calculus (TRC)](#tuple-relational-calculus-trc): Uses tuple variables to represent entire rows of a relation.
  2. [Domain Relational Calculus (DRC)](#domain-relational-calculus-drc): Uses domain variables to represent individual attribute values.
- Both Relational Algebra and Relational Calculus are theoretically equivalent in expressive power for relational queries, provided the calculus queries are restricted to safe expressions.

### Syntax

The general syntax of Relational Calculus is:

$$\{t \mid P(t)\}$$

Where:

- $t$ = tuple or variable representing the required data.
- $\mid$ = “such that”.
- $P(t)$ = predicate or condition that the data must satisfy.


### Example

Consider the `Student` relation:

| ID  | Name | Status |
| --- | ---- | ------ |
| 101 | John | Junior |
| 102 | Lee  | Senior |
| 103 | Mary | Junior |

Requirement: Retrieve the names of all students whose status is `Junior`.

In Relational Calculus, we specify the condition that a student must satisfy rather than describing a sequence of operations.

A Tuple Relational Calculus expression is:

$$\{ t.Name \mid Student(t) \land t.Status='Junior' \}$$

Explanation:

- $t$ is a tuple variable representing a row of the `Student` relation.
- $Student(t)$ means that $t$ belongs to the `Student` relation.
- $t.Status='Junior'$ specifies the condition the tuple must satisfy.
- $t.Name$ identifies the name to return for every tuple satisfying the condition.

Output:

| Name |
| ---- |
| John |
| Mary |

Thus, Relational Calculus retrieves the required data by specifying logical conditions that the data must satisfy.

## Comparison Between Relational Algebra and Relational Calculus

| Relational Algebra                                                                                                            | Relational Calculus                                                                                           |
| ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| 1. It is a procedural query language.                                                                                         | It is a non-procedural query language.                                                                        |
| 2. It specifies how to retrieve the required data.                                                                            | It specifies what data to retrieve.                                                                           |
| 3. It uses operations such as selection $(\sigma)$, projection $(\pi)$, union $(\cup)$, and join $(\bowtie)$. | It uses predicates, logical operators, and quantifiers to define conditions.                                  |
| 4. It is based on set theory and relational operations.                                                                       | It is based on mathematical predicate logic.                                                                  |
| 5. It performs operations on relations to produce a result.                                                                   | It defines conditions that the required tuples or attribute values must satisfy.                              |
| 6. It has no separate types based on tuple and domain variables.                                                              | It has two types: Tuple Relational Calculus (TRC) and Domain Relational Calculus (DRC).                       |
| 7. Its expressions describe a sequence of relational operations.                                                              | Its expressions describe logical conditions for the result.                                                   |
| 8. Example: $\pi_{Name}(\sigma_{Status='Junior'}(Student))$                                                          | Example: $\{t.Name \mid Student(t)\land t.Status='Junior'\}$                                            |
| 9. It is useful for understanding query processing and relational operations.                                                 | It is useful for expressing database queries through logical conditions.                                      |
| 10. It is theoretically equivalent in expressive power to safe Relational Calculus.                                           | It is theoretically equivalent in expressive power to Relational Algebra when restricted to safe expressions. |

Remember:

- Relational Algebra: How to retrieve data.
- Relational Calculus: What data to retrieve.

[Go To Top](#content)

---

# Tuple Relational Calculus (TRC)


- Tuple Relational Calculus (TRC) is a non-procedural query language used to retrieve data from a relational database.
- It uses tuple variables to represent entire rows (tuples) of a relation.
- It specifies the conditions that tuples must satisfy to be included in the result.
- It is based on predicate logic and uses logical operators such as AND $(\land)$, OR $(\lor)$, NOT $(\neg)$, and quantifiers such as existential $(\exists)$ and universal $(\forall)$.
- TRC describes what data is required rather than the sequence of operations needed to retrieve it.

### Syntax

The general syntax of Tuple Relational Calculus is:

$$\{t \mid P(t)\}$$

Where:

- $t$ = tuple variable representing a row of a relation.
- $\mid$ = “such that”.
- $P(t)$ = predicate or condition that the tuple must satisfy.
- The result contains the tuples or specified tuple attributes that satisfy the condition.

### Example

Consider the `Student` relation:

| ID  | Name | Status   |
| --- | ---- | -------- |
| 101 | John | Junior   |
| 102 | Lee  | Senior   |
| 103 | Mary | Junior   |
| 104 | Sam  | Freshman |

Question: Retrieve all students whose status is `Junior`.

TRC expression:

$$\{t \mid Student(t) \land t.Status='Junior'\}$$

Explanation:

- $t$ represents a tuple in the `Student` relation.
- $Student(t)$ ensures that $t$ belongs to the `Student` relation.
- $t.Status='Junior'$ checks whether the student's status is `Junior`.
- Only tuples satisfying the condition are returned.

Output:

| ID  | Name | Status |
| --- | ---- | ------ |
| 101 | John | Junior |
| 103 | Mary | Junior |

### 4. Logical Operators Used in TRC

| Operator      | Meaning      | Example                                                          |
| ------------- | ------------ | ---------------------------------------------------------------- |
| $\land$   | AND          | $t.Status='Junior' \land t.ID>100$                           |
| $\lor$    | OR           | $t.Status='Junior' \lor t.Status='Senior$                   |
| $\neg$    | NOT          | $\neg(t.Status='Junior')$                                    |
| $\exists$ | There exists | $\exists s(Student(s)\land s.Status='Junior')$               |
| $\forall$ | For all      | A condition must hold for every tuple in the specified relation. |

### Examples of TRC Queries

Using the same `Student` relation:

- Example 1: Retrieve the names of all students.

    $\{t.Name \mid Student(t)\}$

    Output: John, Lee, Mary, Sam.

- Example 2: Retrieve students whose ID is greater than 102.

    $\{t \mid Student(t)\land t.ID>102\}$

    Output: Mary and Sam, including their complete tuples.

- Example 3: Retrieve students whose status is either Junior or Senior.

    $\{t \mid Student(t)\land (t.Status='Junior'\lor t.Status='Senior')\}$

    Output: John, Lee, and Mary, including their complete tuples.

- Example 4: Retrieve students whose status is not Junior.

    $\{t \mid Student(t)\land \neg(t.Status='Junior')\}$
    
    Output: Lee and Sam, including their complete tuples.

### 6. Important Properties of TRC

- Non-procedural: Specifies what data is required, not how to retrieve it.
- Tuple variables: Uses variables to represent complete rows of a relation.
- Predicate-based: Retrieves tuples that satisfy specified conditions.
- Logical operators: Supports AND, OR, and NOT.
- Quantifiers: Uses existential $(\exists)$ and universal $(\forall)$ quantifiers to express more complex conditions.
- Safe expressions: Practical TRC queries must be restricted to safe expressions so that results are finite and drawn from the database's active domain.
- Equivalent expressive power: Safe TRC and Relational Algebra have equivalent expressive power.

### 7. Advantages of TRC

- Easy to express queries using logical conditions.
- Useful for representing complex selection criteria.
- Provides a mathematical foundation for database query languages.
- Allows users to specify the required result without defining a sequence of operations.

### 8. Limitations of TRC

- Complex logical expressions can be difficult to understand.
- Unsafe expressions may produce infinite or unbounded results.
- It does not directly specify the procedure for executing a query.
- Queries involving multiple relations and quantifiers can become complicated.

Remember for exams: TRC uses tuple variables and the general syntax $\{t \mid P(t)\}$, where $P(t)$ specifies the condition that the tuple must satisfy.


[Go To Top](#content)

---
# Domain Relational Calculus (DRC)

- Domain Relational Calculus (DRC) is a non-procedural query language used to retrieve data from a relational database.
- It uses domain variables to represent individual attribute values rather than entire rows (tuples).
- It specifies the conditions that attribute values must satisfy to be included in the result.
- It is based on mathematical predicate logic and uses logical operators such as $(\land)$, OR $(\lor)$, NOT $(\neg)$, and quantifiers such as existential $(\exists)$ and universal $(\forall)$.
- Like Tuple Relational Calculus (TRC), DRC specifies what data is required rather than how to retrieve it.

### Syntax

The general syntax of Domain Relational Calculus is:

$$\{ \langle x_1,x_2,\ldots,x_n\rangle \mid P(x_1,x_2,\ldots,x_n)\}$$

Where:

- $x_1,x_2,\ldots,x_n$ = domain variables representing individual attribute values.
- $\langle \ \rangle$ = represents the output tuple containing the required attribute values.
- $\mid$ = “such that”.
- $P(x_1,x_2,\ldots,x_n)$ = predicate or condition that the values must satisfy.

### Example

Consider the `Student` relation:

| ID  | Name | Status   |
| --- | ---- | -------- |
| 101 | John | Junior   |
| 102 | Lee  | Senior   |
| 103 | Mary | Junior   |
| 104 | Sam  | Freshman |

Question: Retrieve the names of all students whose status is `Junior`.

DRC expression:

$$\{ \langle n\rangle \mid \exists i\ ,\exists s, (Student(i,n,s)\land s='Junior')\}$$

Explanation:

- $i$ represents the student's ID.
- $n$ represents the student's name.
- $s$ represents the student's status.
- $Student(i,n,s)$ means that a tuple with these values exists in the `Student` relation.
- $s='Junior'$ checks whether the student's status is `Junior`.
- $\exists i\ ,\exists s$ means there exist values for the ID and status that satisfy the condition.
- Only the name $n$ is returned.

Output:

| Name |
| ---- |
| John |
| Mary |

### Logical Operators Used in DRC

| Operator      | Meaning      | Example                                                                 |
| ------------- | ------------ | ----------------------------------------------------------------------- |
| $\land$   | AND          | $s='Junior'\land i>100$                                             |
| $\lor$   | OR           | $s='Junior'\lor s='Senior'$                                         |
| $\neg$   | NOT          | $\neg(s='Junior')$                                                  |
| $\exists$ | There exists | $\exists i\ ,Student(i,n,s)$                                        |
| $\forall$ | For all      | A condition must hold for every value or tuple in the specified domain. |

### Examples of DRC Queries

Using the same `Student` relation, where the attributes are `(ID, Name, Status)`:

Example 1: Retrieve the names of all students.

$$\{\langle n\rangle \mid \exists i\ ,\exists s,Student(i,n,s)\}$$

Output: John, Lee, Mary, Sam.

Example 2: Retrieve the names of students whose ID is greater than 102.

$$\{ \langle n\rangle \mid \exists i\ ,\exists s, (Student(i,n,s)\land i>102)\}$$

Output: Mary, Sam.

Example 3: Retrieve the names of students whose status is either Junior or Senior.

$$\{\langle n\rangle \mid \exists i\ ,\exists s, (Student(i,n,s)\land (s='Junior'\lor s='Senior'))\}$$

Output: John, Lee, Mary.

Example 4: Retrieve the names of students whose status is not Junior.

$$\{\langle n\rangle \mid \exists i\ ,\exists s, (Student(i,n,s)\land \neg(s='Junior'))\}$$

Output: Lee, Sam.

### Important Properties of DRC

- Non-procedural: Specifies what data is required, not how to retrieve it.
- Domain variables: Uses variables to represent individual attribute values.
- Predicate-based: Retrieves values that satisfy specified conditions.
- Logical operators: Supports AND, OR, and NOT.
- Quantifiers: Uses existential $(\exists)$ and universal $(\forall)$ quantifiers to express complex conditions.
- Safe expressions: Practical DRC queries must be restricted to safe expressions to ensure finite results drawn from the database's active domain.
- Equivalent expressive power: Safe DRC and Relational Algebra have equivalent expressive power.

### Advantages of DRC

- Allows queries to be expressed using conditions on individual attribute values.
- Useful when only selected attributes are required as output.
- Provides a mathematical foundation for database query languages.
- Separates the required result from the procedure used to retrieve it.

### Limitations of DRC

- Complex expressions involving multiple variables and quantifiers can be difficult to understand.
- Unsafe expressions may produce infinite or unbounded results.
- It does not directly specify the steps for executing a query.
- Queries involving multiple relations may require complicated logical conditions.



[Go To Top](#content)

---

# TRC vs DRC

| Tuple Relational Calculus (TRC)                                | Domain Relational Calculus (DRC)                                     |
| -------------------------------------------------------------- | -------------------------------------------------------------------- |
| Uses tuple variables representing entire rows.                 | Uses domain variables representing individual attribute values.      |
| Refers to attributes using tuple variables, e.g. $t.Name$. | Refers to attribute values using individual variables, e.g. $n$. |
| General syntax: $\{t\mid P(t)\}$.                        | General syntax: $\{\langle x_1,\ldots,x_n\rangle\mid P\}$.     |
| Returns tuples or specified tuple attributes.                  | Returns tuples formed from the specified domain variables.           |

Remember for exams: DRC uses domain variables and the general syntax $\{\langle x_1,\ldots,x_n\rangle\mid P\}$, where $P$ defines the conditions the attribute values must satisfy.

[Go To Top](#content)

---
