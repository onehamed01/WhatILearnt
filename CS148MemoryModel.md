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



Hami, your understanding is **mostly correct**, but there are a few **technical inaccuracies and English issues**. I edited your README to keep it **short, clear, and technically precise**, while preserving your original idea.

I also corrected one important misunderstanding about memory.


# Mutability in Python

Some data types are **immutable** (such as `int`, `str`, and `bool`).  
This means their objects **cannot be modified after creation**.  
Instead, when we try to change them, Python **creates a new object**.

Example:

```python
>>> a = "foo"
>>> id(a)
127229567618912

>>> a = "foo" + "apple"
>>> a
'fooapple'

>>> id(a)
127229567613680
````

As we can see, the `id` values are different.
This means Python created a **new object**. This happens because **strings are immutable**.

Note: In the images, objects are represented with double borders.

[https://www.teach.cs.toronto.edu/~csc148h/notes/_images/Immutable-type-crop.jpg](https://www.teach.cs.toronto.edu/~csc148h/notes/_images/Immutable-type-crop.jpg)

---

# Mutable Objects

Mutable types include **list, dict, set, and class instances**.
Mutable objects **can change their internal state without creating a new object**.

Example with immutable type:

```python
a = 10
a = 10 + 23
```

Here `10` is an immutable integer.
The operation creates a **new object (33)** and `a` now refers to that new object.

---

Example with a mutable type:

```python
>>> lst = [1, 3, 4, 2]
>>> id(lst)
127229586524992

>>> lst[0] = 43000
>>> lst
[43000, 3, 4, 2]

>>> id(lst)
127229586524992
```

The `id` of `lst` is the same before and after the modification.
This means the **list object itself did not change**.

However, the element inside the list changed.

---

Example showing this clearly:

```python
>>> lst = [1, 2, 3, 4]

>>> id(lst[0])
11755688

>>> id(lst)
140716187011904

>>> lst[0] = 43000

>>> id(lst[0])
140716167968944

>>> id(lst)
140716187011904
```

Here we can see:

* The `list` object keeps the **same id**.
* The integer at index `0` changed from `1` to `43000`.
* Since integers are **immutable**, Python created a **new integer object**.

Each index in a list **stores a reference to an object**.
When we assign a new value (`43000`), Python creates a new integer object and updates the reference at that index.

The **list object itself remains the same**, but the **reference stored in the index changes**.


