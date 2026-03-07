# Python Memory Model

## Introduction

In Python, all data is stored in **objects**.  
Each object has three fundamental properties:

- **Identity** (`id`)
- **Type**
- **Value**

### Object Identity

Every object has an **identity**, which uniquely identifies it during its lifetime.  
You can inspect an object's identity using the `id()` function.

### Variables and Objects

Variables **do not store data directly**.  
Instead, variables store **references to objects**.

This means a variable is simply a **name that refers to an object in memory**.

Example:

```python
x = 3
word = "bonjour"
````

In this example:

* The object `3` exists in memory
* The object `"bonjour"` exists in memory
* `x` refers to the object `3`
* `word` refers to the object `"bonjour"`

![Memory model preview](https://www.teach.cs.toronto.edu/~csc148h/notes/_images/Variables-crop.jpg)

### Objects Have Types

Variables themselves **do not have types**.

Instead:

* **Objects have types**
* The type determines what operations and methods can be applied to them.

Examples:

* `3` → type `int`
* `"bonjour"` → type `str`


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

Explanation:

When we assign a new value to `cat`, Python does **not modify the original object**.
Instead, the variable `cat` now refers to a **different object**.

The previous object (`"piki"`) remains in memory temporarily until Python's **garbage collector** removes it if no references point to it.


# Assignment Statement

Consider the following assignment:

```python
a = 5 + 3
```

When Python executes this statement, it performs the following steps:

1. **Evaluate the expression on the right-hand side**

```
5 + 3 → 8
```

2. **Find or create the object**

Python locates or creates the object `8`.

3. **Bind the variable on the left-hand side**

The variable `a` is now bound to the object `8`.

Important concepts:

* **Expression → Right-hand side**
* **Variable → Left-hand side**

Assignment in Python **does not copy values**.
Instead, it **binds a variable name to an object**.



## Improvements I made to your content

These were the main conceptual fixes:

### 1. Variables do not store IDs exactly
You wrote that variables store IDs.  
More precisely:

> Variables store **references to objects**.

The `id()` function is just a way for us to inspect identity.


### 2. Object identity wording
Instead of:

> "each object has unique id that no object has one"

The correct idea is:

> Each object has a unique identity **during its lifetime**.

Python may reuse memory later.


### 3. Value change explanation
You originally implied the value changed.

But actually:

```python
cat = "piki"
cat = "dowla"
````

The `"piki"` object is **not modified**.
The variable simply **points to a new object**.

