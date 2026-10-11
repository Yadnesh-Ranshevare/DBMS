# Relational Algebra
---
# Content
1. [Introduction](#introduction)
2. [Selection ](#selection)

---

# Introduction

Relational Algebra is a procedural query language in DBMS used to retrieve and manipulate data stored in relational tables.

It uses mathematical operations to perform queries on tables (relations). It specifies what operations to perform and how to obtain the required data.

For example, if you have a `Student` table and want to retrieve students who scored more than 80 marks, relational algebra provides operations to do that.

### Types of operation in Relational algebra

there are two main type of operator in relational algebra that is:

1. **Fundamental Operators**

    These are the basic operators from which other relational algebra operations can be derived.

    | Sr. No. | Operator          | Symbol       | Purpose                                                           |
    | ------- | ----------------- | ------------ | ----------------------------------------------------------------- |
    | 1       | [Selection](#selection-)         | ($\sigma$) | Selects rows that satisfy a condition.                            |
    | 2       | Projection        | ($\pi$)    | Selects specific columns from a relation.                         |
    | 3       | Union             | ($\cup$)   | Combines tuples from two compatible relations.                    |
    | 4       | Set Difference    | ($-$)      | Returns tuples present in one relation but not the other.         |
    | 5       | Cartesian Product | ($\times$) | Combines every tuple of one relation with every tuple of another. |
    | 6       | Rename            | ($\rho$)   | Renames a relation or its attributes.                             |

2. **Derived Operators**

    These operators can be expressed using fundamental operators or other relational algebra operations.

    | Sr. No. | Operator     | Symbol           | Purpose                                                                        |
    | ------- | ------------ | ---------------- | ------------------------------------------------------------------------------ |
    | 1       | Intersection | ($\cap$)       | Returns tuples common to both relations.                                       |
    | 2       | Join         | ($\bowtie$)    | Combines related tuples from two relations based on a condition.               |
    | 3       | Division     | ($\div$)       | Finds tuples associated with all tuples in another relation.                   |
    | 4       | Assignment   | ($\leftarrow$) | Assigns the result of a relational algebra expression to a temporary relation. |


Note that some textbooks classify assignment separately as an additional convenience operator rather than a derived operator. Follow the classification prescribed by your syllabus or professor.

[Go To Top](#content)

---

# Selection
- it os used to select the rows / tuples of a relation / table
- Unary operator: input as well as output in same relation / table
- Since the row don't have any name in the table so to select the rows we've to apply certain condition or predicate
- It can return one or many rows / tuples based on condition
- if no condition is given it will return the whole relation / table

### Syntax:

$$\sigma_p(R)$$

where:
- $\sigma$ = selection operator
- p = condition
- R = relation / table

### Example:
input Student table:
| Id | Name | Address | Status |
| --- | --- | --- | --- | 
| 1123 | John | 123 Main | Junior | 
| 1234 | Lee | 123 Main | Senior | 
| 5556 | Mary | 7 Lake Dr | Freshman | 
| 9876 | Bart | 5 pine St | Junior |

operation:
    
$$\sigma_{Status = 'Junior'}(Student)$$

output:
| Id | Name | Address | Status |
| --- | --- | --- | --- | 
| 1123 | John | 123 Main | Junior | 
| 9876 | Bart | 5 pine St | Junior |


you can chain the selection operation::
    
$$\sigma_{Id = 1123}(\sigma_{Status = 'Junior'}(Student))$$

output:
| Id | Name | Address | Status |
| --- | --- | --- | --- | 
| 1123 | John | 123 Main | Junior | 

### How the chaining work

- when you write $\sigma_{p}(R)$ it return a relation / table
- let assume it return relation / table $R_o$ 
- now you just pass this new relation / table $R_o$ as input in next selection operation
- that is next operation became $\sigma_{p_o}(R_o)$
- here:
    - $P_o$ = new condition
    - $R_o$ = new relation
- Mathematically
    $$\sigma_{p}(R) = R_o$$
    Therefore
    $$\sigma_{p_o}(R_o) = \sigma{p_o}(\sigma_p(R))$$

We can generalize this:

$$\sigma_{p_n}(\sigma_{p_{n-1}}(\sigma_{p_{n-2}}(R)))$$

you can chain as much as you want

### Another Representation

because of this chaining property we can use logical AND ($\land$) instead of chaining syntax 

new syntax:

$$\sigma_{p_1 \land p_2}(R) = \sigma_{p1}(\sigma_{p_2}(R))$$

Or

$$\sigma_{p_1 \ AND\ p_2}(R) = \sigma_{p1}(\sigma_{p_2}(R))$$

### Selection operation are commutative:
in selection operation the order of applying selection operations does not affect the final result.

That is:

$$\sigma_{p_1}(\sigma_{p_2}(R)) = \sigma_{p_2}(\sigma_{p_1}(R))$$

Or

$$\sigma_{p_1 \land p_2}(R)  = \sigma_{p_2 \land p_1}(R)$$

[Go To Top](#content)

---