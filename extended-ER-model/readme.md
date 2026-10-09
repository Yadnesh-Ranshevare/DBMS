# Content

1. [Generalization / specialization](#generalization--specialization)

---

# Generalization / specialization

In DBMS, Generalization and Specialization are concepts used in an ER diagram to represent relationships between a general entity and its more specific types.

**Symbol: Triangle**

> Generalization and specialization use the same symbol, and the difference is the direction of the relationship, not the symbol.

### 1. Generalization

Generalization is a bottom-up approach in which two or more similar entities are combined into one common, higher-level entity based on their shared attributes.

Example

Suppose we have two entities:

- `Car`: Registration_No, Color
- `Bike`: Registration_No, Color

Both share common attributes, so we create a generalized entity called `Vehicle`.

Why?\
Instead of defining the same common attributes separately for Car and Bike, we put them in the common entity `Vehicle`.

### 2. Specialization

Specialization is a top-down approach in which one higher-level entity is divided into two or more lower-level entities based on their specific characteristics.

Example

Suppose we have a general entity called `Employee`, with attributes `Employee_ID` and `Name`.

We divide it into two specialized entities:

- Manager: Bonus
- Developer: Programming_Language

Why?\
All employees share common attributes, but managers and developers can have their own additional attributes.

Both `Manager` and `Developer` inherit the common attributes of Employee.

### Attribute Inheritance
Attribute inheritance means that a specialize entity(sub class) automatically receives the attributes of its generalize entity (superclass).

**Example**

Suppose we have a superclass `Employee` and two subclasses, `Manager` and `Developer`.
Here:
- Employee has `Employee_ID`, `Name`, and `Salary`.
- Manager inherits all three attributes and has its own additional attribute, `Bonus`.
- Developer inherits all three attributes and has its own additional attribute, `Programming_Language`.

Therefore, a Manager doesn't need to redefine `Employee_ID`, `Name`, and `Salary`.

> Specialize entity does not have instance of their own, out all of the generalize entity we separate out the specialize entity into different type

### Participation Inheritance
Participation inheritance means that a specialize entity (subclass) inherits the participation constraints of its generalize entity (superclass) in an ER diagram.

In simple words, if a superclass participates in a relationship, its subclass also participates in that relationship because every subclass entity is also a member of the superclass.

**Example**

Suppose we have a superclass `Employee` and a subclass `Manager`.

- Every `Employee` must work in a `Department`.
- `Manager` is a subclass of `Employee`.

Therefore, every `Manager` must also work in a `Department`, because every manager is an employee.

### Generalization vs Specialization

<img src="./img/Generalization-specialization.png" style="background:white; padding:10; width:500px"/>

here

- `Person` -> generalize entity
- `Student` / `Teacher` -> specialize entity

| Generalization                      | Specialization                      |
| ----------------------------------- | ----------------------------------- |
| Bottom-up approach                  | Top-down approach                   |
| Combines multiple entities          | Divides one entity                  |
| Identifies common features          | Identifies specific features        |
| Example: student + TEacher → Person | Example: Person → Student + Teacher |

[Go To Top](#content)

---
