# Relational Algebra
---
# Content
1. [Introduction](#introduction)
2. [Selection Operator](#selection-operator)
3. [Projection Operator](#projection-operator)
4. [Union Operator](#union-operator)
5. [Set Difference Operator](#set-difference-operator)

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
    | 1       | [Selection](#selection-operator)         | ($\sigma$) | Selects rows that satisfy a condition.                            |
    | 2       | [Projection](#projection-operator)        | ($\pi$)    | Selects specific columns from a relation.                         |
    | 3       | [Union](#union-operator)             | ($\cup$)   | Combines tuples from two compatible relations.                    |
    | 4       | [Set Difference](#set-difference-operator)    | ($-$)      | Returns tuples present in one relation but not the other.         |
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

# Selection Operator
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
# Projection Operator

- It is used to select specific columns / attributes of a relation / table.
- Unary operator: input as well as output is a relation / table.
- Since a table contains multiple attributes (columns), projection is used to specify which attributes we want in the output.
- It can return one or many columns / attributes based on the attributes specified.
- If all attributes are specified, it returns the entire relation with all columns.
- Duplicate rows are eliminated in relational algebra because relations are sets.

### Syntax

$$\pi_{A_1,A_2,\ldots,A_n}(R)$$

where:

- $\pi$ = projection operator
- $A_1,A_2,\ldots,A_n$ = attributes / columns to be selected
- $R$ = relation / table

### Example

Input Student table:

| Id   | Name | Address   | Status   |
| ---- | ---- | --------- | -------- |
| 1123 | John | 123 Main  | Junior   |
| 1234 | Lee  | 123 Main  | Senior   |
| 5556 | Mary | 7 Lake Dr | Freshman |
| 9876 | Bart | 5 Pine St | Junior   |

Operation:

$$\pi_{Name,Status}(Student)$$

Output:

| Name | Status   |
| ---- | -------- |
| John | Junior   |
| Lee  | Senior   |
| Mary | Freshman |
| Bart | Junior   |

Here, only the `Name` and `Status` columns are included in the output. The remaining columns are removed.
### Projection removes duplicates

- In relational algebra, projection removes duplicate rows / tuples from the output.
- If two or more rows have the same values for the selected attributes, only **one copy** of that row is retained.
- This happens because relational algebra treats relations as sets, and a set cannot contain duplicate elements.

Let's continue with the previous example.

**Operation:**


$$\pi_{Name,Status}(Student)$$


**Output:**

| Name | Status |
|---|---|
| John | Junior |
| Lee | Senior |
| Mary | Freshman |
| Bart | Junior |

Note that the `Status` column contains two entries with the value `Junior`. However, these rows are not duplicates because their `Name` values are different.

**Now, let's apply another projection operation:**


$$\pi_{Status}(\pi_{Name,Status}(Student))$$

**Output:**

| Status |
|---|
| Junior |
| Senior |
| Freshman |

As you can see, the duplicate value `Junior` appears only once in the output.

**Explanation:**

- The first projection selects the `Name` and `Status` columns.
- The second projection selects only the `Status` column, removing the `Name` column.
- Since both `John` and `Bart` have the status `Junior`, their resulting tuples become identical.
- Therefore, only one occurrence of `Junior` is retained.

**Important:** Duplicate removal occurs based on the complete set of selected attributes, not on individual column values unless that column is the only selected attribute. 

### How projection works

- When you write $\pi_{A_1,A_2}(R)$, it returns a new relation containing only the specified attributes.
- Let us assume the resulting relation is $R_o$.
- You can pass this new relation as input to another projection operation, provided the next operation uses attributes that still exist in the resulting relation.

Mathematically:

$$\pi_{Name,Status}(Student)=R_o$$

Therefore,

$$\pi_{Status}(R_o)$$

can be written as:

$$\pi_{Status}(\pi_{Name,Status}(Student))$$

Output:

| Status |
|---|
| Junior |
| Senior |
| Freshman |

You can chain projection operations, but selecting fewer columns in an earlier operation means those removed columns cannot be selected in a later operation.

### Another representation

Because of the chaining property, multiple projection operations can be simplified into a single projection operation.

For example:

$$\pi_{Name}(\pi_{Name,Status}(Student))$$

can be simplified to:

$$\pi_{Name}(Student)$$

In general:

$$\pi_A(\pi_B(R))=\pi_A(R)$$

provided that $A\subseteq B$, meaning every attribute in $A$ is also present in $B$.

### Projection operations are idempotent

Applying the same projection operation more than once does not change the result.

That is:

$$\pi_A(\pi_A(R))=\pi_A(R)$$

For example:

$$\pi_{Name}(\pi_{Name}(Student)) =\pi_{Name}(Student)$$

The output remains the same because the `Name` column has already been selected.

### Difference between Selection and Projection

| Selection $(\sigma)$                                                      | Projection $(\pi)$                     |
| ----------------------------------------------------------------------------- | ------------------------------------------ |
| Selects rows / tuples                                                         | Selects columns / attributes               |
| Uses a condition or predicate                                                 | Specifies attribute names                  |
| Can reduce the number of rows                                                 | Can reduce the number of columns           |
| Duplicate rows are not independently retained in set-based relational algebra | Duplicate rows are eliminated              |
| Example: $\sigma\_{Status='Junior'}(Student)$                            | Example: $\pi\_{Name,Status}(Student)$ |

Remember this shortcut:

- $\sigma$ (Selection) → Rows
- $\pi$ (Projection) → Columns

[Go To Top](#content)

---
# Union Operator

- It is used to combine the rows / tuples of two relations / tables into a single relation / table.
- It is a binary operator, meaning it takes two relations as input and produces one relation as output.
- The union operation returns all tuples that are present in either relation or in both relations.
- Duplicate rows are eliminated because relational algebra treats relations as sets.
- The two relations must be union-compatible to perform the union operation.

### Syntax

$$R \cup S$$

where:

- $\cup$ = union operator
- $R$ = first relation / table
- $S$ = second relation / table

### What is union compatibility?

Two relations are union-compatible if:

- Both relations have the same number of attributes (columns).
- The corresponding attributes have compatible domains / data types.

For example, if `Student1` has three columns — `Id`, `Name`, and `Status` — then `Student2` must also have three corresponding compatible columns.

### Example

Input `Student1` table:

| Id   | Name | Status   |
| ---- | ---- | -------- |
| 1123 | John | Junior   |
| 1234 | Lee  | Senior   |
| 5556 | Mary | Freshman |

Input `Student2` table:

| Id   | Name | Status   |
| ---- | ---- | -------- |
| 5556 | Mary | Freshman |
| 9876 | Bart | Junior   |
| 2222 | Sam  | Senior   |

Operation:

$$Student1 \cup Student2$$

Output:

| Id   | Name | Status   |
| ---- | ---- | -------- |
| 1123 | John | Junior   |
| 1234 | Lee  | Senior   |
| 5556 | Mary | Freshman |
| 9876 | Bart | Junior   |
| 2222 | Sam  | Senior   |

### Explanation

- All tuples from `Student1` and `Student2` are combined.
- The tuple `(5556, Mary, Freshman)` appears in both relations.
- Since union eliminates duplicate tuples, this tuple appears only once in the output.
- The order of tuples in the output does not matter.

### Union removes duplicates

Consider the following operation:

$$Student1 \cup Student2$$

Both relations contain the tuple:

$$(5556,\ Mary,\ Freshman)$$

After applying union, this tuple appears only once.

Important: Duplicate removal applies to the entire tuple, not to individual column values. For example, two students can have the same `Status` and still remain separate tuples if their other attribute values differ.

### Union is commutative

The order of the relations does not affect the final result.

$$R \cup S = S \cup R$$

For example:

$$Student1 \cup Student2 = Student2 \cup Student1$$

Both operations produce the same set of tuples.

### Union is associative

When combining three or more relations, the grouping does not affect the final result.

$$(R \cup S) \cup T = R \cup (S \cup T)$$

Therefore, you can chain multiple union operations:

$$R \cup S \cup T$$

provided that all relations are union-compatible.

### Union with itself

Taking the union of a relation with itself produces the same relation because duplicate tuples are eliminated.

$$R \cup R = R$$


Remember: Union means combining rows from two compatible relations, retaining each distinct tuple only once.


[Go To Top](#content)

---
# Set Difference Operator

- It is used to retrieve the rows / tuples that are present in one relation / table but not present in the other relation / table.
- It is a binary operator, meaning it takes two relations as input and produces one relation as output.
- The set difference operation returns only those tuples that exist in the first relation but do not exist in the second relation.
- Duplicate rows are eliminated because relational algebra treats relations as sets.
- The two relations must be union-compatible to perform the set difference operation.

### Syntax

$$R-S$$

where:

- $-$ = set difference operator
- $R$ = first relation / table
- $S$ = second relation / table

Important: Set difference is directional. $R-S$ and $S-R$ generally produce different results.

### Both relation / table must be compatible

Two relations are compatible if:

- Both relations have the same number of attributes (columns).
- The corresponding attributes have compatible domains / data types.

For example, if `Student1` has three columns — `Id`, `Name`, and `Status` — then `Student2` must also have three corresponding compatible columns.



### Example

Input `Student1` table:

| Id   | Name | Status   |
| ---- | ---- | -------- |
| 1123 | John | Junior   |
| 1234 | Lee  | Senior   |
| 5556 | Mary | Freshman |
| 9876 | Bart | Junior   |

Input `Student2` table:

| Id   | Name | Status   |
| ---- | ---- | -------- |
| 5556 | Mary | Freshman |
| 9876 | Bart | Junior   |
| 2222 | Sam  | Senior   |

Operation:

$$Student1-Student2$$

Output:

| Id   | Name | Status |
| ---- | ---- | ------ |
| 1123 | John | Junior |
| 1234 | Lee  | Senior |

### Explanation

- First, consider all tuples present in `Student1`.
- Check whether each tuple also exists in `Student2`.
- If a tuple exists in both relations, remove it from the result.
- If a tuple exists in `Student1` but not in `Student2`, retain it.
- Therefore, only John and Lee appear in the output.

### Reverse the operation

Now, let's reverse the relations.

Operation:

$$Student2-Student1$$

Output:

| Id   | Name | Status |
| ---- | ---- | ------ |
| 2222 | Sam  | Senior |

Explanation:

Sam exists in `Student2` but does not exist in `Student1`. Therefore, Sam is the only tuple in the result.

This demonstrates that:

$$R-S \neq S-R$$

in general.

### Set difference is not commutative

Unlike union, changing the order of the relations can change the result.

$$R-S \neq S-R$$

For example:

$$Student1-Student2$$

returns John and Lee, whereas:

$$Student2-Student1$$

returns Sam.

### Set difference is not associative

Changing the grouping of set difference operations can change the result.

$$(R-S)-T \neq R-(S-T)$$

in general.

Therefore, you cannot arbitrarily change the grouping of multiple set difference operations.

### Set difference with itself

If we subtract a relation from itself, no tuples remain.

$$R-R=\varnothing$$

where $\varnothing$ represents the empty relation.


### Quick comparison

| Operator                 | Purpose                                                         |
| ------------------------ | --------------------------------------------------------------- |
| Union ($\cup$)       | Returns tuples present in either relation                       |
| Set Difference ($-$) | Returns tuples present in the first relation but not the second |

Remember: $R-S$ means keep the tuples in $R$ and remove those that also exist in $S$.



[Go To Top](#content)

---
# Cartesian Product Operator

- It is used to combine every row / tuple of one relation with every row / tuple of another relation.
- It is a binary operator, meaning it takes two relations as input and produces one relation as output.
- Each tuple of the first relation is paired with every tuple of the second relation.
- The resulting relation contains all possible combinations of tuples from the two input relations.
- If relation $R$ contains $m$ tuples and relation $S$ contains $n$ tuples, the resulting relation contains $m \times n$ tuples.
- The number of attributes in the output is the sum of the number of attributes in both input relations.

### Syntax

$$R \times S$$

where:

- $\times$ = Cartesian product operator
- $R$ = first relation / table
- $S$ = second relation / table

### Example

Input `Student` table:

| Student_ID | Name |
| ---------- | ---- |
| 101        | John |
| 102        | Lee  |

Input `Course` table:

| Course_ID | Course_Name |
| --------- | ----------- |
| C1        | DBMS        |
| C2        | Java        |
| C3        | Python      |

Operation:

$$Student \times Course$$

Output:

| Student_ID | Name | Course_ID | Course_Name |
| ---------- | ---- | --------- | ----------- |
| 101        | John | C1        | DBMS        |
| 101        | John | C2        | Java        |
| 101        | John | C3        | Python      |
| 102        | Lee  | C1        | DBMS        |
| 102        | Lee  | C2        | Java        |
| 102        | Lee  | C3        | Python      |

### How Cartesian product works

- Take the first tuple from `Student` (John).
- Combine it with every tuple in `Course`, producing three tuples.
- Take the next tuple from `Student` (Lee).
- Again, combine it with every tuple in `Course`, producing three more tuples.
- Combine all the resulting tuples to form the output relation.

Therefore, the output contains six tuples.

$$|Student \times Course| =|Student|\times|Course|$$

$$=2\times3=6$$

Here, $|R|$ represents the number of tuples in relation $R$.

### Number of rows and columns in Cartesian product

If relation $R$ has $m$ rows and $a$ columns, and relation $S$ has $n$ rows and $b$ columns, then:

- Number of rows: $m\times n$
- Number of columns: $a+b$

For example, if $R$ has 3 rows and 2 columns, while $S$ has 4 rows and 3 columns:

$$\text{Rows}=3\times4=12$$

$$\text{Columns}=2+3=5$$

The output relation will contain 12 rows and 5 columns.

### Cartesian product can generate duplicate-looking rows

- The Cartesian product generates every possible combination of tuples from both relations.
- If two resulting tuples are identical across all attributes, relational algebra retains only one copy because relations are sets.
- However, in the usual case where each input relation has distinct tuples and their attributes are kept separately identifiable, the output contains exactly $m\times n$ tuples.

### Cartesian product does not require union compatibility

Unlike union and set difference, Cartesian product does not require both relations to have the same number of attributes or matching attribute domains.

For example, `Student` can have two attributes and `Course` can have three attributes. Their Cartesian product is still valid, producing five attributes.

### Cartesian product is not commutative in its schema

In general:

$$R\times S\neq S\times R$$

The tuple combinations correspond to the same pairings, but the attribute order differs: $R\times S$ places the attributes of $R$ before those of $S$, while $S\times R$ does the reverse.

### Cartesian product is associative

For relations with appropriately handled attribute names and ordering:

$$(R\times S)\times T = R\times(S\times T)$$

Both expressions generate all possible combinations of tuples from the three relations.

### Cartesian product with an empty relation

If either input relation is empty, the result is empty.

$$R\times\varnothing=\varnothing$$

This is because there are no tuples available in the empty relation to form combinations.

### Quick comparison

| Operator                         | Purpose                                                                   |
| -------------------------------- | ------------------------------------------------------------------------- |
| Union ($\cup$)               | Combines tuples from two relations and eliminates duplicates              |
| Set Difference ($-$)         | Returns tuples in the first relation but not the second                   |
| Cartesian Product ($\times$) | Combines every tuple of the first relation with every tuple of the second |

Remember: Cartesian product means every row of $R$ paired with every row of $S$. If one table has 4 rows and the other has 5 rows, the result has $4\times5=20$ tuples.


[Go To Top](#content)

---