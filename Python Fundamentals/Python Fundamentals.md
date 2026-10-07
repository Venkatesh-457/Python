# Python Fundamentals

Python Fundamentals covers the basic rules and concepts required to write, understand, and execute Python programs. These foundations are important before moving into advanced topics such as OOP.

---

## 1. Program Structure and Execution

Python programs consist of statements that are executed in order.

```python
print("Hello")
print("World")
print("Python")
```

Output:

```text
Hello
World
Python
```

Python generally executes statements from top to bottom unless a control structure changes the flow.

---

## 2. Statements

A **statement** is an instruction that Python executes.

Examples:

```python
x = 10
print(x)
```

Here:

* `x = 10` → assignment statement
* `print(x)` → function-call statement

Python normally does not require `;` at the end of every statement.

```python
x = 10
y = 20
print(x + y)
```

---

## 3. Variables

A variable is a **name that refers to a value/object**.

```python
x = 10
```

Here:

* `x` → variable name
* `10` → value/object being referred to
* `=` → assignment

A variable can be reassigned:

```python
x = 10
x = 20

print(x)
```

Output:

```text
20
```

### Variable assignment

```python
name = "Venkat"
age = 20
marks = 85
```

### Multiple assignment

Different values can be assigned to multiple variables:

```python
x, y, z = 10, 20, 30
```

Equivalent to:

```text
x → 10
y → 20
z → 30
```

The same value can also be assigned to multiple variables:

```python
x = y = z = 10
```

### Important

Python variables should be mentally understood as **names referring to objects**, rather than boxes permanently containing values.

The deeper concept of references, objects, and identity is covered separately later in the roadmap.

---

## 4. `print()`

`print()` is used to display output.

```python
print("Hello")
print(10)
print(10 + 20)
```

Output:

```text
Hello
10
30
```

Variables can also be printed:

```python
name = "Venkat"
age = 20

print(name)
print(age)
```

### Printing multiple values

```python
x = 10
y = 20

print(x, y, x + y)
```

Output:

```text
10 20 30
```

By default, `print()` places a space between multiple values.

### `sep`

`sep` controls what is placed between multiple values.

```python
print(10, 20, 30, sep="-")
```

Output:

```text
10-20-30
```

### `end`

`print()` normally moves to the next line after printing.

```python
print("Hello")
print("World")
```

Output:

```text
Hello
World
```

The default value of `end` is a newline.

It can be changed:

```python
print("Hello", end=" ")
print("World")
```

Output:

```text
Hello World
```

---

## 5. `input()`

`input()` is used to receive input from the user.

```python
name = input("Enter your name: ")
print(name)
```

If the user enters:

```text
Venkat
```

the program prints:

```text
Venkat
```

### Important: `input()` returns a string

Even if the user enters a number:

```python
age = input("Enter your age: ")
```

and enters:

```text
20
```

the value received by `age` is the string:

```python
"20"
```

Therefore:

```python
x = input()
y = input()

print(x + y)
```

If the user enters `10` and `10`, the result is:

```text
1010
```

because string concatenation occurs.

To perform numerical addition, conversion is required:

```python
x = int(input())
y = int(input())

print(x + y)
```

Type conversion is covered in detail under **Data Types & Type Conversion**.

---

## 6. Expressions

An **expression** is something Python can evaluate to produce a value.

Examples:

```python
10 + 20
```

produces:

```text
30
```

```python
x * 2
```

produces a value based on `x`.

Even individual values can be expressions:

```python
10
"Hello"
```

### Expression inside a statement

```python
x = 10 + 5
```

Here:

* `10 + 5` → expression
* `x = 10 + 5` → assignment statement

The expression produces `15`, which is then assigned to `x`.

### Simple distinction

```text
Expression → produces/evaluates to a value
Statement  → performs an instruction
```

---

## 7. Indentation and Blocks

Python uses **indentation to define blocks of code**.

```python
if x > 5:
    print("A")
    print("B")

print("C")
```

The two indented `print()` statements belong to the `if` block.

```text
if x > 5:
    ├── print("A")
    └── print("B")

print("C")
```

### The colon `:`

A colon indicates that a block is about to begin.

```python
if x > 5:
    print("Greater")
```

The same structure is used with constructs such as:

```python
if condition:
    ...

for item in items:
    ...

while condition:
    ...

def function():
    ...

class Student:
    ...
```

### Nested blocks

Blocks can exist inside other blocks:

```python
if x > 5:
    print("A")

    if x > 10:
        print("B")
```

The inner block is further indented.

### Important

Python normally uses **4 spaces** for one indentation level.

Indentation is not merely visual formatting in Python. It is part of the language syntax.

---

## 8. Comments

Comments are ignored by Python and are mainly used to explain code.

### Single-line comment

```python
# This is a comment
print("Hello")
```

A comment can also appear beside code:

```python
x = 10  # storing 10 in x
```

---

## 9. Case Sensitivity

Python is **case-sensitive**.

These are different names:

```python
name
Name
NAME
```

Example:

```python
name = "Venkat"
Name = "Ravi"

print(name)
print(Name)
```

Output:

```text
Venkat
Ravi
```

Therefore, variable names, function names, class names, etc. must be written with the correct capitalization.

---

## 10. Python Keywords

**Keywords** are reserved words that have special meaning in Python.

They cannot be used as normal variable names.

Invalid:

```python
return = 10
```

Invalid:

```python
class = 10
```

Valid:

```python
return_value = 10
my_class = 10
```

Some commonly encountered Python keywords include:

```text
if
else
elif
for
while
def
class
return
import
from
try
except
True
False
None
and
or
not
in
is
```

Python's `keyword` module can be used to check whether a word is a keyword:

```python
import keyword

print(keyword.iskeyword("class"))
```

Output:

```text
True
```

---

## 11. Basic Types of Errors

Python programs can encounter different kinds of errors.

### 11.1 Syntax Error

Occurs when the code does not follow Python's syntax rules.

Example:

```python
if x > 10
    print(x)
```

The `:` is missing.

---

### 11.2 Runtime Error

The code is syntactically valid, but an error occurs while the program is running.

Example:

```python
x = 10
y = 0

print(x / y)
```

Division by zero causes a runtime error.

---

### 11.3 Logical Error

The program runs successfully, but the logic is incorrect and produces an unintended result.

Example:

```python
a = 10
b = 20

print(a - b)
```

Python executes this successfully, but if the intended operation was addition, the logic is wrong.

### Summary

```text
Syntax Error  → Python cannot understand the code structure
Runtime Error → Error occurs during execution
Logical Error → Program runs but produces the wrong result
```

---

## 12. Naming Conventions

Python allows many valid names, but following conventions makes code easier to read.

### Variables and functions → `snake_case`

```python
student_name = "Venkat"
total_marks = 450
calculate_average()
```

### Constants → `UPPER_CASE`

```python
PI = 3.14159
MAX_SIZE = 100
```

Uppercase is a convention indicating that a value is intended to be treated as a constant. Python does not technically prevent it from being changed.

### Classes → `PascalCase`

```python
Student
BankAccount
CarEngine
```

This convention becomes particularly important in OOP.

---

# Quick Revision

```text
Python Fundamentals
│
├── Program execution
├── Statements
├── Variables
├── print()
├── input()
├── Expressions
├── Indentation & blocks
├── Comments
├── Case sensitivity
├── Keywords
├── Basic error types
└── Naming conventions
```

## Most Important Things to Remember

1. **Python executes statements in order.**
2. **Variables are names that refer to objects/values.**
3. **`print()` displays output.**
4. **`input()` returns a string.**
5. **An expression evaluates to a value.**
6. **A statement is an instruction executed by Python.**
7. **Indentation defines code blocks in Python.**
8. **`:` starts a block in constructs such as `if`, `for`, `def`, and `class`.**
9. **Python is case-sensitive.**
10. **Keywords cannot be used as normal variable names.**
11. **Syntax, runtime, and logical errors are different types of problems.**
12. **Use `snake_case` for variables/functions and `PascalCase` for classes.**
