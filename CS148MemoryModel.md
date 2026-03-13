# Python Memory Model

## Introduction

In Python, all data is stored in **objects**.  
Each object has three fundamental properties:

- **Identity** (`id`)
- **Type**
- **Value**

---

## Object Identity

Every object has an **identity**, which uniquely identifies it during its lifetime.

You can inspect an object's identity using:

```python
id(object)
````

---

## Variables and Objects

Variables **do not store data directly**.
Instead, variables store **references to objects**.

A variable is simply a **name bound to an object in memory**.

Example:

```python
x = 3
word = "bonjour"
```

In this example:

* The object `3` exists in memory
* The object `"bonjour"` exists in memory
* `x` refers to the object `3`
* `word` refers to the object `"bonjour"`

![Python Memory Model](https://www.teach.cs.toronto.edu/~csc148h/notes/_images/Variables-crop.jpg)

---

## Objects Have Types

Variables themselves **do not have types**.

Instead:

* **Objects have types**
* The type determines which operations and methods can be applied.

Examples:

* `3` → `int`
* `"bonjour"` → `str`

---

# Object Identity Example

```python
cat = "piki"
print(id(cat))

cat = "dowla"
print(id(cat))
```

Example output:

```
132435450774560
132435450787760
```

### Explanation

When a new value is assigned to `cat`, Python does **not modify the original object**.

Instead:

* The variable `cat` now refers to a **different object**
* The previous object (`"piki"`) remains in memory temporarily
* Python may later remove it using **garbage collection** if no references point to it

---

# Assignment Statement

Consider the following assignment:

```python
a = 5 + 3
```

When Python executes this statement, it performs the following steps:

### 1. Evaluate the right-hand side expression

```
5 + 3 → 8
```

### 2. Find or create the object

Python locates or creates the object `8`.

### 3. Bind the variable on the left-hand side

The variable `a` is now bound to the object `8`.

Key idea:

* **Expression → Right-hand side**
* **Variable → Left-hand side**

Assignment in Python **does not copy values**.
Instead, it **binds a variable name to an object**.

---

# Mutability in Python

Some Python types are **immutable**, such as:

* `int`
* `str`
* `bool`
* `tuple`

Immutable objects **cannot be modified after creation**.
When a change appears to occur, Python actually **creates a new object**.

Example:

```python
a = "foo"
print(id(a))

a = "foo" + "apple"
print(a)
print(id(a))
```

Example result:

```
fooapple
```

The `id` values are different, which means Python created a **new object**.

![Immutable Objects](https://www.teach.cs.toronto.edu/~csc148h/notes/_images/Immutable-type-crop.jpg)

---

# Mutable Objects

Mutable types include:

* `list`
* `dict`
* `set`
* class instances

Mutable objects **can change their internal state without creating a new object**.

Example:

```python
lst = [1, 3, 4, 2]
print(id(lst))

lst[0] = 43000
print(lst)

print(id(lst))
```

Output shows the **same id** before and after modification.

This means the **list object itself did not change**, but its **internal state did**.

---

## Example Showing Reference Changes

```python
lst = [1, 2, 3, 4]

print(id(lst[0]))
print(id(lst))

lst[0] = 43000

print(id(lst[0]))
print(id(lst))
```

What happens here:

* The **list object keeps the same id**
* The element at index `0` changes
* Since integers are **immutable**, Python creates a **new integer object**

Each index in a list **stores a reference to an object**.

When a new value is assigned, Python:

1. Creates a new object (if needed)
2. Updates the reference stored in that index

The **list object itself remains the same**, but the **reference inside the list changes**.
